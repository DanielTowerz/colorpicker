<script lang="ts">
	let baseColor = $state('#3b82f6');
	let surfaceLightness = $state(1.2);
	let brandLightness = $state(3);
	let brandChroma = $state(5);
	let textOpacity = $state(0.6);

	// Initialize theme on component mount
	$effect(() => {
		updateTheme();
	});

	function getLightnessFromHex(hex: string): number {
		const hexCode = hex.replace('#', '');
		const r = parseInt(hexCode.substr(0, 2), 16);
		const g = parseInt(hexCode.substr(2, 2), 16);
		const b = parseInt(hexCode.substr(4, 2), 16);
		
		const brightness = (r * 0.299 + g * 0.587 + b * 0.114);
		return (brightness / 255) * 100;
	}

	function hexToOklch(hex: string): string {
		// Convert HEX to RGB first
		const hexCode = hex.replace('#', '');
		const r = parseInt(hexCode.substr(0, 2), 16) / 255;
		const g = parseInt(hexCode.substr(2, 2), 16) / 255;
		const b = parseInt(hexCode.substr(4, 2), 16) / 255;
		
		// Convert RGB to linear RGB
		const toLinear = (c: number) => c <= 0.04045 ? c / 12.92 : Math.pow((c + 0.055) / 1.055, 2.4);
		const rLinear = toLinear(r);
		const gLinear = toLinear(g);
		const bLinear = toLinear(b);
		
		// Convert linear RGB to XYZ (using D65 illuminant)
		const x = 0.4124564 * rLinear + 0.3575761 * gLinear + 0.1804375 * bLinear;
		const y = 0.2126729 * rLinear + 0.7151522 * gLinear + 0.0721750 * bLinear;
		const z = 0.0193339 * rLinear + 0.1191920 * gLinear + 0.9503041 * bLinear;
		
		// Convert XYZ to OKLab
		const l_ = Math.cbrt(0.8189330101 * x + 0.3618667424 * y - 0.1288597137 * z);
		const m_ = Math.cbrt(0.0329845436 * x + 0.9293118715 * y + 0.0361456387 * z);
		const s_ = Math.cbrt(0.0482003018 * x + 0.2643662691 * y + 0.6338517070 * z);
		
		const l = 0.2104542553 * l_ + 0.7936177850 * m_ - 0.0040720468 * s_;
		const a = 1.9779984951 * l_ - 2.4285922050 * m_ + 0.4505937099 * s_;
		const b_oklab = 0.0259040371 * l_ + 0.7827717662 * m_ - 0.8086757660 * s_;
		
		// Convert OKLab to OKLCH
		const lightness = l;
		const chroma = Math.sqrt(a * a + b_oklab * b_oklab);
		let hue = Math.atan2(b_oklab, a) * 180 / Math.PI;
		if (hue < 0) hue += 360;
		
		// Return OKLCH values with proper precision
		return `oklch(${(lightness * 100).toFixed(2)}% ${chroma.toFixed(4)} ${hue.toFixed(2)})`;
	}

	function updateTheme() {
		const lightness = getLightnessFromHex(baseColor);
		const textColor = lightness > 60 ? '#000000' : '#ffffff';
		const baseColorOklch = hexToOklch(baseColor);
		
		document.body.style.setProperty('--base-color', baseColorOklch);
		document.body.style.setProperty('--surface-color', `oklch(from var(--base-color) calc(l * ${surfaceLightness}) c h)`);
		document.body.style.setProperty('--surface-light', `oklch(from var(--surface-color) calc(l * 1.2) c h)`);
		document.body.style.setProperty('--brand-color', `oklch(from var(--base-color) calc(l * ${brandLightness}) calc(c * ${brandChroma}) h)`);
		document.body.style.setProperty('--text-color', textColor);
		document.body.style.setProperty('--text-secondary', `oklch(from var(--text-color) l c h / ${textOpacity})`);
	}

	function setColor(inputElement: HTMLInputElement) {
		baseColor = inputElement.value;
		updateTheme();
	}

	function updateSurfaceLightness(value: number) {
		surfaceLightness = value;
		updateTheme();
	}

	function updateBrandLightness(value: number) {
		brandLightness = value;
		updateTheme();
	}

	function updateBrandChroma(value: number) {
		brandChroma = value;
		updateTheme();
	}

	function updateTextOpacity(value: number) {
		textOpacity = value;
		updateTheme();
	}

	function generateThemeId(): string {
		const timestamp = Date.now();
		const colorHex = baseColor.replace('#', '');
		return `theme-${colorHex}-${timestamp}`;
	}

	function generateCSSContent(): string {
		const lightness = getLightnessFromHex(baseColor);
		const textColor = lightness > 60 ? '#000000' : '#ffffff';
		const baseColorOklch = hexToOklch(baseColor);
		const themeId = generateThemeId();
		const currentDate = new Date().toLocaleString();
		
		return `/* 
 * Generated Theme: ${themeId}
 * Base Color: ${baseColor} (converted to OKLCH: ${baseColorOklch})
 * Surface Lightness: ${surfaceLightness}
 * Brand Lightness: ${brandLightness}, Chroma: ${brandChroma}
 * Text Opacity: ${textOpacity}
 * Generated on: ${currentDate}
 * Theme Picker Component - Dynamic Color System
 */

.${themeId} {
	/* Base theme color chosen by user */
	--base-color: ${baseColorOklch};
	
	/* Surface color - ${surfaceLightness}x lightness of base */
	--surface-color: oklch(from var(--base-color) calc(l * ${surfaceLightness}) c h);
	
	/* Surface light - 20% brighter than surface color for cards */
	--surface-light: oklch(from var(--surface-color) calc(l * 1.2) c h);
	
	/* Brand color - ${brandLightness}x lightness, ${brandChroma}x chroma for emphasis */
	--brand-color: oklch(from var(--base-color) calc(l * ${brandLightness}) calc(c * ${brandChroma}) h);
	
	/* Text color - automatically adjusted for contrast */
	--text-color: ${textColor};
	
	/* Secondary text - ${textOpacity} opacity of main text color */
	--text-secondary: oklch(from var(--text-color) l c h / ${textOpacity});
	
	/* Additional utility colors */
	--border-color: oklch(from var(--base-color) calc(l * 1.4) c h);
	--hover-surface: oklch(from var(--surface-color) calc(l * 1.2) c h);
	--shadow-color: oklch(from var(--base-color) calc(l * 0.8) c h / 0.3);
	
	/* Apply base styles */
	background-color: var(--base-color);
	color: var(--text-color);
	transition: background-color 0.3s ease, color 0.3s ease;
}

/* Component styles for the theme */
.${themeId} .card {
	background-color: var(--surface-color);
	border: 1px solid var(--border-color);
	border-radius: 0.75rem;
	padding: 1.5rem;
	transition: all 0.3s ease;
}

.${themeId} .card:hover {
	transform: translateY(-2px);
	box-shadow: 0 8px 25px var(--shadow-color);
}

.${themeId} .btn-primary {
	background-color: var(--brand-color);
	color: var(--text-color);
	border: none;
	padding: 0.75rem 1.5rem;
	border-radius: 0.5rem;
	font-weight: 600;
	cursor: pointer;
	transition: all 0.3s ease;
}

.${themeId} .btn-primary:hover {
	background-color: oklch(from var(--brand-color) calc(l * 1.1) c h);
	transform: translateY(-1px);
}

.${themeId} .btn-secondary {
	background-color: var(--hover-surface);
	color: var(--text-color);
	border: 1px solid var(--border-color);
	padding: 0.75rem 1.5rem;
	border-radius: 0.5rem;
	font-weight: 600;
	cursor: pointer;
	transition: all 0.3s ease;
}

.${themeId} .btn-secondary:hover {
	background-color: oklch(from var(--hover-surface) calc(l * 1.1) c h);
	transform: translateY(-1px);
}

.${themeId} .input-field {
	background-color: var(--hover-surface);
	color: var(--text-color);
	border: 1px solid var(--border-color);
	padding: 0.75rem 1rem;
	border-radius: 0.5rem;
	transition: all 0.3s ease;
}

.${themeId} .input-field:focus {
	outline: none;
	border-color: var(--brand-color);
	box-shadow: 0 0 0 3px oklch(from var(--brand-color) l c h / 0.2);
}

/* Text utilities */
.${themeId} .text-primary {
	color: var(--text-color);
}

.${themeId} .text-secondary {
	color: var(--text-secondary);
}

/* Blog Card Styles */
.${themeId} .blog-card {
	background-color: var(--surface-light);
	border-radius: 1rem;
	overflow: hidden;
	border: 1px solid oklch(from var(--base-color) calc(l * 1.5) c h);
	transition: all 0.3s ease;
	display: flex;
	flex-direction: column;
	height: 100%;
}

.${themeId} .blog-card:hover {
	transform: translateY(-4px);
	box-shadow: 0 12px 32px oklch(from var(--base-color) calc(l * 0.8) c h / 0.2);
}

.${themeId} .blog-image {
	height: 200px;
	background: oklch(from var(--surface-color) calc(l * 0.9) c h);
	display: flex;
	align-items: center;
	justify-content: center;
	border-bottom: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h / 0.3);
}

.${themeId} .blog-content {
	padding: 1.5rem;
	display: flex;
	flex-direction: column;
	flex: 1;
}

.${themeId} .blog-category {
	background-color: var(--brand-color);
	color: var(--text-color);
	padding: 0.25rem 0.75rem;
	border-radius: 1rem;
	font-size: 0.75rem;
	font-weight: 600;
	text-transform: uppercase;
	letter-spacing: 0.05em;
}

.${themeId} .blog-title {
	font-size: 1.25rem;
	font-weight: 700;
	line-height: 1.4;
	margin-bottom: 0.75rem;
	color: var(--text-color);
}

.${themeId} .author-avatar {
	width: 2.5rem;
	height: 2.5rem;
	border-radius: 50%;
	background-color: var(--brand-color);
	display: flex;
	align-items: center;
	justify-content: center;
	font-weight: 600;
	font-size: 0.875rem;
	color: var(--text-color);
}

.${themeId} .read-more-btn {
	background: transparent;
	border: 2px solid var(--brand-color);
	color: var(--brand-color);
	padding: 0.5rem 1rem;
	border-radius: 0.5rem;
	font-weight: 600;
	font-size: 0.875rem;
	cursor: pointer;
	transition: all 0.3s ease;
}

.${themeId} .read-more-btn:hover {
	background-color: var(--brand-color);
	color: var(--text-color);
	transform: translateY(-1px);
}

/* Usage Instructions:
 * 1. Add the class "${themeId}" to your body or container element
 * 2. Use the provided CSS custom properties in your styles
 * 3. Apply component classes like .card, .btn-primary, etc.
 * 
 * Example:
 * <body class="${themeId}">
 *   <div class="card">
 *     <h2 class="text-primary">Card Title</h2>
 *     <p class="text-secondary">Card description</p>
 *     <button class="btn-primary">Action</button>
 *   </div>
 * </body>
 */`;
	}

	function exportTheme() {
		const cssContent = generateCSSContent();
		const themeId = generateThemeId();
		const filename = `${themeId}.css`;
		
		const blob = new Blob([cssContent], { type: 'text/css' });
		const url = URL.createObjectURL(blob);
		
		const link = document.createElement('a');
		link.href = url;
		link.download = filename;
		link.style.display = 'none';
		
		document.body.appendChild(link);
		link.click();
		document.body.removeChild(link);
		
		URL.revokeObjectURL(url);
	}
</script>

<div class="theme-picker">
	<div class="picker-header">
		<label for="base-color-input" class="text-sm font-medium text-[oklch(from_var(--text-color)_l_c_h)]">
			Background Color
		</label>
		<input
			id="base-color-input"
			type="color"
			value={baseColor}
			oninput={(e) => setColor(e.currentTarget)}
			class="w-12 h-8 rounded border-2 border-[oklch(from_var(--base-color)_calc(l*1.2)_c_h)] cursor-pointer"
		/>
	</div>

	<div class="controls-section">
		<h3 class="text-sm font-semibold text-[oklch(from_var(--text-color)_l_c_h)] mb-3">Theme Adjustments</h3>
		
		<div class="control-group">
			<label class="control-label">
				Surface Lightness: {surfaceLightness.toFixed(1)}
			</label>
			<input
				type="range"
				min="0.5"
				max="2.0"
				step="0.1"
				value={surfaceLightness}
				oninput={(e) => updateSurfaceLightness(parseFloat(e.currentTarget.value))}
				class="range-input"
			/>
		</div>

		<div class="control-group">
			<label class="control-label">
				Brand Lightness: {brandLightness.toFixed(1)}
			</label>
			<input
				type="range"
				min="1.0"
				max="5.0"
				step="0.1"
				value={brandLightness}
				oninput={(e) => updateBrandLightness(parseFloat(e.currentTarget.value))}
				class="range-input"
			/>
		</div>

		<div class="control-group">
			<label class="control-label">
				Brand Chroma: {brandChroma.toFixed(1)}
			</label>
			<input
				type="range"
				min="1.0"
				max="10.0"
				step="0.1"
				value={brandChroma}
				oninput={(e) => updateBrandChroma(parseFloat(e.currentTarget.value))}
				class="range-input"
			/>
		</div>

		<div class="control-group">
			<label class="control-label">
				Text Opacity: {textOpacity.toFixed(1)}
			</label>
			<input
				type="range"
				min="0.1"
				max="1.0"
				step="0.05"
				value={textOpacity}
				oninput={(e) => updateTextOpacity(parseFloat(e.currentTarget.value))}
				class="range-input"
			/>
		</div>
	</div>
	
	<div class="export-section">
		<button
			onclick={exportTheme}
			class="export-button"
			title="Export current theme as CSS file"
		>
			<svg 
				class="w-4 h-4" 
				fill="none" 
				stroke="currentColor" 
				viewBox="0 0 24 24"
			>
				<path 
					stroke-linecap="round" 
					stroke-linejoin="round" 
					stroke-width="2" 
					d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
				></path>
			</svg>
			Export Theme
		</button>
		
		<div class="theme-info">
			<span class="color-preview" style="background-color: {baseColor}"></span>
			<span class="color-value text-[color:var(--text-secondary)]">
				{baseColor.toUpperCase()}
			</span>
		</div>
	</div>
</div>

<style>
	:global(body) {
		--base-color: oklch(67.07% 0.1540 252.42);
		--surface-color: oklch(from var(--base-color) calc(l * 1.2) c h);
		--surface-light: oklch(from var(--surface-color) calc(l * 1.2) c h);
		--brand-color: oklch(from var(--base-color) calc(l * 3) calc(c * 5) h);
		--text-secondary: oklch(from var(--text-color) l c h / 0.6);
		--text-color: #ffffff;
		
		background-color: var(--base-color);
		color: var(--text-color);
		transition: background-color 0.3s ease, color 0.3s ease;
	}

	.theme-picker {
		display: flex;
		flex-direction: column;
		gap: 1rem;
		padding: 0;
		background: transparent;
		border: none;
		border-radius: 0;
		width: 100%;
		min-width: auto;
	}

	.controls-section {
		display: flex;
		flex-direction: column;
		gap: 1rem;
		border-top: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h / 0.3);
		padding-top: 1rem;
		margin-top: 1rem;
	}

	.control-group {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}

	.control-label {
		font-size: 0.875rem;
		font-weight: 500;
		color: oklch(from var(--text-color) l c h);
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.range-input {
		width: 100%;
		height: 6px;
		border-radius: 3px;
		background: oklch(from var(--surface-color) calc(l * 1.2) c h);
		outline: none;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.range-input::-webkit-slider-thumb {
		appearance: none;
		width: 18px;
		height: 18px;
		border-radius: 50%;
		background: var(--brand-color);
		cursor: pointer;
		border: 2px solid oklch(from var(--text-color) l c h);
		box-shadow: 0 2px 6px oklch(from var(--base-color) calc(l * 0.8) c h / 0.3);
		transition: all 0.3s ease;
	}

	.range-input::-webkit-slider-thumb:hover {
		background: oklch(from var(--brand-color) calc(l * 1.1) c h);
		transform: scale(1.1);
	}

	.range-input::-moz-range-thumb {
		width: 18px;
		height: 18px;
		border-radius: 50%;
		background: var(--brand-color);
		cursor: pointer;
		border: 2px solid oklch(from var(--text-color) l c h);
		box-shadow: 0 2px 6px oklch(from var(--base-color) calc(l * 0.8) c h / 0.3);
		transition: all 0.3s ease;
	}

	.picker-header {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}

	.export-section {
		display: flex;
		flex-direction: column;
		gap: 0.75rem;
		border-top: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h / 0.3);
		padding-top: 1rem;
		margin-top: 1rem;
	}

	.export-button {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		background-color: var(--brand-color);
		color: var(--text-color);
		padding: 0.75rem 1rem;
		border-radius: 0.5rem;
		border: none;
		font-weight: 600;
		font-size: 0.875rem;
		cursor: pointer;
		transition: all 0.3s ease;
		justify-content: center;
	}

	.export-button:hover {
		background-color: oklch(from var(--brand-color) calc(l * 1.1) c h);
		transform: translateY(-1px);
		box-shadow: 0 4px 12px oklch(from var(--brand-color) l c h / 0.3);
	}

	.theme-info {
		display: flex;
		align-items: center;
		gap: 0.75rem;
		padding: 0.5rem;
		background-color: oklch(from var(--surface-color) calc(l * 1.1) c h);
		border-radius: 0.5rem;
		border: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h / 0.5);
	}

	.color-preview {
		width: 1.5rem;
		height: 1.5rem;
		border-radius: 0.25rem;
		border: 2px solid oklch(from var(--text-color) l c h / 0.2);
		flex-shrink: 0;
	}

	.color-value {
		font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', monospace;
		font-size: 0.875rem;
		font-weight: 500;
	}

	input[type="color"] {
		appearance: none;
		-webkit-appearance: none;
		border: none;
		cursor: pointer;
	}

	input[type="color"]::-webkit-color-swatch-wrapper {
		padding: 0;
		border: none;
		border-radius: 4px;
	}

	input[type="color"]::-webkit-color-swatch {
		border: none;
		border-radius: 4px;
	}
</style>