<script lang="ts">
	import "../app.css";
	import ThemePicker from "$lib/ThemePicker.svelte";
	
	let sidebarOpen = $state(false);
	
	function toggleSidebar() {
		sidebarOpen = !sidebarOpen;
	}
</script>

<!-- Mobile Toggle Button -->
<button class="sidebar-toggle" onclick={toggleSidebar}>
	<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
		<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 100 4m0-4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 100 4m0-4v2m0-6V4"></path>
	</svg>
</button>

<!-- Fixed Theme Picker Sidebar -->
<aside class="theme-sidebar" class:sidebar-open={sidebarOpen}>
	<div class="sidebar-content">
		<h2 class="sidebar-title text-[oklch(from_var(--text-color)_l_c_h)]">Theme Control</h2>
		<ThemePicker />
	</div>
</aside>

<main class="main-content">
	<div class="content-wrapper">
		<header class="text-center space-y-4">
			<h1 class="text-4xl font-bold text-[oklch(from_var(--text-color)_l_c_h)]">
				Dynamic Theme Picker
			</h1>
			<p class="text-lg text-[oklch(from_var(--text-color)_l_c_h_/_0.6)]">
				Choose any background color and watch the entire interface adapt
				automatically
			</p>
		</header>

		<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
			<div class="card">
				<h3
					class="text-xl font-semibold mb-3 text-[oklch(from_var(--text-color)_l_c_h)]"
				>
					Surface Container
				</h3>
				<p class="text-[oklch(from_var(--text-color)_l_c_h_/_0.6)] mb-4">
					This container uses the surface color, which is automatically 20%
					brighter than the base color.
				</p>
				<button class="btn-primary"> Brand Button </button>
			</div>

			<div class="card">
				<h3
					class="text-xl font-semibold mb-3 text-[oklch(from_var(--text-color)_l_c_h)]"
				>
					Another Card
				</h3>
				<p class="text-[oklch(from_var(--text-color)_l_c_h_/_0.6)] mb-4">
					Notice how the text color automatically switches between black and
					white for optimal readability.
				</p>
				<button class="btn-secondary"> Secondary Action </button>
			</div>

			<div class="card">
				<h3
					class="text-xl font-semibold mb-3 text-[oklch(from_var(--text-color)_l_c_h)]"
				>
					Relative Colors
				</h3>
				<p class="text-[oklch(from_var(--text-color)_l_c_h_/_0.6)] mb-4">
					All colors are calculated relative to your chosen base color using
					OKLCH color space.
				</p>
				<button class="btn-outline"> Outlined Button </button>
			</div>
		</div>

		<!-- Blog Post Card Example -->
		<div class="blog-section">
			<h2 class="text-2xl font-bold mb-6 text-[oklch(from_var(--text-color)_l_c_h)]">
				Blog Post Card Example
			</h2>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-6">
				<article class="blog-card">
					<div class="blog-image">
						<div class="placeholder-image">
							<svg class="w-12 h-12 text-[oklch(from_var(--text-color)_l_c_h_/_0.4)]" fill="currentColor" viewBox="0 0 20 20">
								<path fill-rule="evenodd" d="M4 3a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V5a2 2 0 00-2-2H4zm12 12H4l4-8 3 6 2-4 3 6z" clip-rule="evenodd"></path>
							</svg>
						</div>
					</div>
					<div class="blog-content">
						<div class="blog-meta">
							<span class="blog-category">Technology</span>
							<time class="blog-date text-[oklch(from_var(--text-color)_l_c_h_/_0.6)]">
								Jan 15, 2025
							</time>
						</div>
						<h3 class="blog-title text-[oklch(from_var(--text-color)_l_c_h)]">
							The Future of Dynamic Color Systems
						</h3>
						<p class="blog-excerpt text-[oklch(from_var(--text-color)_l_c_h_/_0.7)]">
							Explore how modern web applications are leveraging OKLCH color space 
							and relative color functions to create adaptive, accessible interfaces 
							that respond to user preferences in real-time.
						</p>
						<div class="blog-footer">
							<div class="author-info">
								<div class="author-avatar">
									<span class="text-[oklch(from_var(--text-color)_l_c_h)]">JD</span>
								</div>
								<span class="author-name text-[oklch(from_var(--text-color)_l_c_h_/_0.8)]">
									Jane Doe
								</span>
							</div>
							<button class="read-more-btn">
								Read More
							</button>
						</div>
					</div>
				</article>

				<article class="blog-card">
					<div class="blog-image">
						<div class="placeholder-image">
							<svg class="w-12 h-12 text-[oklch(from_var(--text-color)_l_c_h_/_0.4)]" fill="currentColor" viewBox="0 0 20 20">
								<path d="M3 4a1 1 0 011-1h12a1 1 0 011 1v2a1 1 0 01-1 1H4a1 1 0 01-1-1V4zM3 10a1 1 0 011-1h6a1 1 0 011 1v6a1 1 0 01-1 1H4a1 1 0 01-1-1v-6zM14 9a1 1 0 00-1 1v6a1 1 0 001 1h2a1 1 0 001-1v-6a1 1 0 00-1-1h-2z"></path>
							</svg>
						</div>
					</div>
					<div class="blog-content">
						<div class="blog-meta">
							<span class="blog-category">Design</span>
							<time class="blog-date text-[oklch(from_var(--text-color)_l_c_h_/_0.6)]">
								Jan 12, 2025
							</time>
						</div>
						<h3 class="blog-title text-[oklch(from_var(--text-color)_l_c_h)]">
							Building Accessible Theme Systems
						</h3>
						<p class="blog-excerpt text-[oklch(from_var(--text-color)_l_c_h_/_0.7)]">
							Learn the principles behind creating theme systems that automatically 
							adjust contrast ratios and maintain accessibility standards across 
							different color combinations.
						</p>
						<div class="blog-footer">
							<div class="author-info">
								<div class="author-avatar">
									<span class="text-[oklch(from_var(--text-color)_l_c_h)]">AS</span>
								</div>
								<span class="author-name text-[oklch(from_var(--text-color)_l_c_h_/_0.8)]">
									Alex Smith
								</span>
							</div>
							<button class="read-more-btn">
								Read More
							</button>
						</div>
					</div>
				</article>
			</div>
		</div>

		<div class="demo-section">
			<h2
				class="text-2xl font-bold mb-4 text-[oklch(from_var(--text-color)_l_c_h)]"
			>
				Interactive Demo
			</h2>
			<div class="space-y-4">
				<div class="flex items-center gap-4">
					<label class="text-[oklch(from_var(--text-color)_l_c_h)]"
						>Sample Input:</label
					>
					<input
						type="text"
						placeholder="Type something..."
						class="input-field"
					/>
				</div>

				<div class="flex items-center gap-4">
					<label class="text-[oklch(from_var(--text-color)_l_c_h)]"
						>Sample Range:</label
					>
					<input type="range" min="0" max="100" value="50" class="slider" />
				</div>
			</div>
		</div>
	</div>
</main>

<style>
	/* Fixed Sidebar Styles */
	.theme-sidebar {
		position: fixed;
		top: 0;
		right: 0;
		height: 100vh;
		width: 380px;
		background-color: var(--surface-color);
		border-left: 2px solid oklch(from var(--base-color) calc(l * 1.4) c h);
		z-index: 1000;
		overflow-y: auto;
		transition: all 0.3s ease;
	}

	.sidebar-content {
		padding: 2rem 1.5rem;
		height: 100%;
		display: flex;
		flex-direction: column;
	}

	.sidebar-title {
		font-size: 1.5rem;
		font-weight: 700;
		margin-bottom: 1.5rem;
		text-align: center;
	}

	/* Main Content Adjustments */
	.main-content {
		margin-right: 380px;
		min-height: 100vh;
		padding: 2rem;
		transition: margin-right 0.3s ease;
	}

	.content-wrapper {
		max-width: 1200px;
		margin: 0 auto;
		space-y: 3rem;
	}

	.content-wrapper > * {
		margin-bottom: 3rem;
	}

	/* Responsive Design */
	@media (max-width: 1024px) {
		.theme-sidebar {
			width: 320px;
		}
		
		.main-content {
			margin-right: 320px;
		}
	}

	@media (max-width: 768px) {
		.theme-sidebar {
			transform: translateX(100%);
			width: 100%;
			max-width: 380px;
		}

		.theme-sidebar.sidebar-open {
			transform: translateX(0);
		}

		.main-content {
			margin-right: 0;
		}

		.sidebar-toggle {
			position: fixed;
			top: 1rem;
			right: 1rem;
			z-index: 1001;
			background-color: var(--brand-color);
			color: var(--text-color);
			border: none;
			border-radius: 50%;
			width: 3rem;
			height: 3rem;
			display: flex;
			align-items: center;
			justify-content: center;
			cursor: pointer;
			box-shadow: 0 4px 12px oklch(from var(--base-color) calc(l * 0.8) c h / 0.3);
			transition: all 0.3s ease;
		}

		.sidebar-toggle:hover {
			transform: scale(1.1);
		}
	}

	@media (min-width: 769px) {
		.sidebar-toggle {
			display: none;
		}
	}

	.card {
		background-color: var(--surface-color);
		padding: 1.5rem;
		border-radius: 0.75rem;
		border: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h);
		transition: all 0.3s ease;
	}

	.card:hover {
		transform: translateY(-2px);
		box-shadow: 0 8px 25px oklch(from var(--base-color) calc(l * 0.8) c h / 0.3);
	}

	.btn-primary {
		background-color: var(--brand-color);
		color: var(--text-color);
		padding: 0.75rem 1.5rem;
		border-radius: 0.5rem;
		border: none;
		font-weight: 600;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.btn-primary:hover {
		background-color: oklch(from var(--brand-color) calc(l * 1.1) c h);
		transform: translateY(-1px);
	}

	.btn-secondary {
		background-color: oklch(from var(--surface-color) calc(l * 1.2) c h);
		color: var(--text-color);
		padding: 0.75rem 1.5rem;
		border-radius: 0.5rem;
		border: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h);
		font-weight: 600;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.btn-secondary:hover {
		background-color: oklch(from var(--surface-color) calc(l * 1.3) c h);
		transform: translateY(-1px);
	}

	.btn-outline {
		background-color: transparent;
		color: var(--text-color);
		padding: 0.75rem 1.5rem;
		border-radius: 0.5rem;
		border: 2px solid var(--brand-color);
		font-weight: 600;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.btn-outline:hover {
		background-color: var(--brand-color);
		transform: translateY(-1px);
	}

	.demo-section {
		background-color: var(--surface-color);
		padding: 2rem;
		border-radius: 0.75rem;
		border: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h);
	}

	.input-field {
		background-color: oklch(from var(--surface-color) calc(l * 1.2) c h);
		color: var(--text-color);
		border: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h);
		padding: 0.75rem 1rem;
		border-radius: 0.5rem;
		transition: all 0.3s ease;
		flex: 1;
		max-width: 300px;
	}

	.input-field:focus {
		outline: none;
		border-color: var(--brand-color);
		box-shadow: 0 0 0 3px oklch(from var(--brand-color) l c h / 0.2);
	}

	.slider {
		background-color: oklch(from var(--surface-color) calc(l * 1.2) c h);
		border-radius: 0.5rem;
		flex: 1;
		max-width: 300px;
	}

	.slider::-webkit-slider-thumb {
		background-color: var(--brand-color);
		border-radius: 50%;
	}

	.slider::-moz-range-thumb {
		background-color: var(--brand-color);
		border-radius: 50%;
		border: none;
	}

	/* Blog Card Styles */
	.blog-section {
		margin-top: 3rem;
	}

	.blog-card {
		background-color: var(--surface-light);
		border-radius: 1rem;
		overflow: hidden;
		border: 1px solid oklch(from var(--base-color) calc(l * 1.5) c h);
		transition: all 0.3s ease;
		display: flex;
		flex-direction: column;
		height: 100%;
	}

	.blog-card:hover {
		transform: translateY(-4px);
		box-shadow: 0 12px 32px oklch(from var(--base-color) calc(l * 0.8) c h / 0.2);
	}

	.blog-image {
		height: 200px;
		background: oklch(from var(--surface-color) calc(l * 0.9) c h);
		display: flex;
		align-items: center;
		justify-content: center;
		border-bottom: 1px solid oklch(from var(--base-color) calc(l * 1.4) c h / 0.3);
	}

	.placeholder-image {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
	}

	.blog-content {
		padding: 1.5rem;
		display: flex;
		flex-direction: column;
		flex: 1;
	}

	.blog-meta {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 1rem;
	}

	.blog-category {
		background-color: var(--brand-color);
		color: var(--text-color);
		padding: 0.25rem 0.75rem;
		border-radius: 1rem;
		font-size: 0.75rem;
		font-weight: 600;
		text-transform: uppercase;
		letter-spacing: 0.05em;
	}

	.blog-date {
		font-size: 0.875rem;
		font-weight: 500;
	}

	.blog-title {
		font-size: 1.25rem;
		font-weight: 700;
		line-height: 1.4;
		margin-bottom: 0.75rem;
	}

	.blog-excerpt {
		font-size: 0.95rem;
		line-height: 1.6;
		margin-bottom: 1.5rem;
		flex: 1;
	}

	.blog-footer {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-top: auto;
	}

	.author-info {
		display: flex;
		align-items: center;
		gap: 0.75rem;
	}

	.author-avatar {
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

	.author-name {
		font-size: 0.875rem;
		font-weight: 500;
	}

	.read-more-btn {
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

	.read-more-btn:hover {
		background-color: var(--brand-color);
		color: var(--text-color);
		transform: translateY(-1px);
	}
</style>
