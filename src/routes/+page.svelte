<script lang="ts">
	import { onMount } from 'svelte';
	let isLoaded = $state(false);

	onMount(() => {
		isLoaded = true;
	});
</script>

<svelte:head>
	<title>ta3alam.app</title>
	<meta
		name="description"
		content="Seamlessly manage your courses, distribute assignments, and track class progress all in one place."
	/>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div class="landing-container" class:loaded={isLoaded}>
	<header class="navbar">
		<div class="logo">
			<span class="logo-text">ta3alam.app</span>
		</div>
		<nav class="nav-links">
			<a
				href="https://github.com/vanillaiice/ta3alam"
				target="_blank"
				rel="noopener noreferrer"
				class="nav-link">Source Code</a
			>
			<a href="/contact" class="nav-link">Contact</a>
		</nav>
	</header>

	<main class="hero-section">
		<div class="hero-content">
			<div class="badge">Beta - Still in development</div>
			<h1 class="hero-title">Welcome to Ta3alam</h1>
			<p class="hero-subtitle">
				The unified platform for teaching and learning, especially for non-traditional education
				systems. Seamlessly manage your courses, distribute assignments, and track class progress
				all in one place.
			</p>
		</div>
	</main>

	<section class="features-section">
		<div class="features-container">
			<h2 class="section-title">Everything you need to succeed</h2>
			<div class="features-grid">
				<div class="feature-card">
					<h3>Course Management</h3>
					<p>
						Organize your classes with structured modules, comprehensive lesson contents, and simple
						scheduling.
					</p>
				</div>

				<div class="feature-card">
					<h3>Assignments & Grading</h3>
					<p>
						Create assignments, accept student submissions in various formats (including native
						in-app audio recording), and provide meaningful feedback directly.
					</p>
				</div>

				<div class="feature-card">
					<h3>Role-Based Access</h3>
					<p>
						Specialized views and actions tailored specifically for Teachers and Students to ensure
						a focused learning environment.
					</p>
				</div>

				<div class="feature-card">
					<h3>Stay Connected</h3>
					<p>
						Keep everyone on the same page with class announcements, synchronized rosters, and
						active communication.
					</p>
				</div>
			</div>
		</div>
	</section>

	<footer class="footer">
		<p>Copyright © {new Date().getFullYear()} vanillaiice</p>
		<p style="margin-top: 0.5rem; color: #888;">
			Licensed under the GNU Affero General Public License v3.0
		</p>
	</footer>
</div>

<style>
	/* Base & Reset Styles */
	:global(body) {
		margin: 0;
		padding: 0;
		font-family:
			'Inter',
			-apple-system,
			BlinkMacSystemFont,
			'Segoe UI',
			Roboto,
			Helvetica,
			Arial,
			sans-serif;
		background-color: #e9e7e7; /* daisyUI garden base-100 */
		color: #100f0f; /* daisyUI garden base-content */
		line-height: 1.5;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}

	:global(*) {
		box-sizing: border-box;
	}

	:global(a) {
		color: inherit;
		text-decoration: none;
	}

	/* Animations */
	@keyframes fadeInUp {
		from {
			opacity: 0;
			transform: translateY(20px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	/* Layout */
	.landing-container {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		overflow-x: hidden;
		opacity: 0;
		transition: opacity 0.5s ease-in;
	}

	.landing-container.loaded {
		opacity: 1;
	}

	/* Navbar */
	.navbar {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 1.5rem 5%;
		position: sticky;
		top: 0;
		z-index: 100;
	}

	.logo {
		font-size: 1.1rem;
		font-weight: 500;
	}

	.logo-text {
		color: #100f0f;
	}

	.nav-links {
		display: flex;
		align-items: center;
		gap: 2rem;
	}

	.nav-link {
		font-size: 0.9rem;
		font-weight: 500;
		color: #5d5656;
		transition: color 0.2s ease;
	}

	.nav-link:hover {
		color: #100f0f;
	}

	.login-link {
		color: #100f0f;
		display: flex;
		align-items: center;
	}

	/* Buttons */
	.btn-primary {
		background: #ff007f;
		color: white;
		padding: 0.6rem 1.5rem;
		border-radius: 8px;
		font-weight: 600;
		font-size: 0.95rem;
		border: none;
		transition: all 0.2s ease;
		display: inline-flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
	}

	.btn-primary:hover {
		transform: translateY(-2px);
		background: #e60073;
		box-shadow: 0 4px 12px rgba(255, 0, 127, 0.3);
	}

	.btn-primary.large {
		padding: 0.8rem 2rem;
		font-size: 1.05rem;
	}

	/* Hero Section */
	.hero-section {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 6rem 5% 6rem;
		text-align: center;
		flex: 1;
	}

	.hero-content {
		max-width: 650px;
		animation: fadeInUp 0.8s ease-out forwards;
	}

	.badge {
		display: inline-block;
		padding: 0.4rem 1rem;
		background: #fae5e5; /* daisyUI garden accent */
		color: #ff007f;
		border-radius: 20px;
		font-size: 0.85rem;
		font-weight: 600;
		margin-bottom: 1.5rem;
	}

	.hero-title {
		font-size: 3rem;
		font-weight: 800;
		line-height: 1.1;
		margin-bottom: 1.5rem;
		color: #100f0f;
		letter-spacing: -0.02em;
	}

	.hero-subtitle {
		font-size: 1.1rem;
		color: #5d5656;
		margin-bottom: 2.5rem;
		line-height: 1.6;
	}

	.cta-group {
		display: flex;
		justify-content: center;
	}

	/* Features Section */
	.features-section {
		background-color: #d1cccc; /* daisyUI garden base-200 */
		padding: 6rem 5%;
		width: 100%;
	}

	.features-container {
		max-width: 1200px;
		margin: 0 auto;
		text-align: center;
	}

	.section-title {
		font-size: 2rem;
		font-weight: 700;
		margin-bottom: 3rem;
		color: #100f0f;
	}

	.features-grid {
		display: grid;
		grid-template-columns: 1fr;
		gap: 2rem;
	}

	@media (min-width: 768px) {
		.features-grid {
			grid-template-columns: repeat(2, 1fr);
		}
	}

	.feature-card {
		background: #e9e7e7; /* daisyUI garden base-100 */
		border-radius: 12px;
		padding: 2.5rem 2rem;
		text-align: left;
		box-shadow:
			0 4px 6px -1px rgba(0, 0, 0, 0.05),
			0 2px 4px -1px rgba(0, 0, 0, 0.03);
		transition: transform 0.3s ease;
	}

	.feature-card:hover {
		transform: translateY(-5px);
	}

	.feature-card h3 {
		font-size: 1.25rem;
		font-weight: 700;
		color: #ff007f;
		margin-top: 0;
		margin-bottom: 1rem;
	}

	.feature-card p {
		color: #5d5656;
		margin: 0;
		line-height: 1.6;
		font-size: 0.95rem;
	}

	/* Footer */
	.footer {
		padding: 2rem 5%;
		background-color: #e9e7e7;
		text-align: center;
		color: #5d5656;
		font-size: 0.85rem;
	}
</style>
