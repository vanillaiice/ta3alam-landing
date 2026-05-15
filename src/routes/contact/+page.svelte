<script lang="ts">
	import { onMount } from 'svelte';
	let isLoaded = $state(false);

	onMount(() => {
		isLoaded = true;
	});
</script>

<svelte:head>
	<title>Contact | ta3alam.app</title>
	<meta name="description" content="Contact the team behind ta3alam.app." />
</svelte:head>

<div class="landing-container" class:loaded={isLoaded}>
	<header class="navbar">
		<div class="logo">
			<a href="/" class="logo-link"><span class="logo-text">ta3alam.app</span></a>
		</div>
		<nav class="nav-links">
			<a href="/" class="nav-link">Home</a>
		</nav>
	</header>

	<main class="hero-section">
		<div class="hero-content" style="text-align: center; margin: 0 auto;">
			<h1 class="hero-title">Get in Touch</h1>
			<p class="hero-subtitle">
				We'd love to hear from you. Whether you have a question, feature request, or just want to
				say hi!
			</p>

			<div class="contact-cards">
				<a href="mailto:vanillaiice1@proton.me" class="contact-card">
					<div class="contact-icon">
						<svg
							viewBox="0 0 24 24"
							width="32"
							height="32"
							stroke="currentColor"
							stroke-width="2"
							fill="none"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"
							></path>
							<polyline points="22,6 12,13 2,6"></polyline>
						</svg>
					</div>
					<h3>Email Us</h3>
					<p>vanillaiice1@proton.me</p>
				</a>

				<a
					href="https://github.com/vanillaiice/ta3alam"
					target="_blank"
					rel="noopener noreferrer"
					class="contact-card"
				>
					<div class="contact-icon">
						<svg
							viewBox="0 0 24 24"
							width="32"
							height="32"
							stroke="currentColor"
							stroke-width="2"
							fill="none"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<path
								d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
							></path>
						</svg>
					</div>
					<h3>GitHub Repository</h3>
					<p>View the source code and contribute</p>
				</a>
			</div>
		</div>
	</main>

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
		background-color: #e9e7e7;
		color: #100f0f;
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

	/* Hero Section */
	.hero-section {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 4rem 5% 6rem;
		flex: 1;
	}

	.hero-content {
		max-width: 800px;
		animation: fadeInUp 0.8s ease-out forwards;
	}

	.hero-title {
		font-size: 3rem;
		font-weight: 800;
		margin-bottom: 1.5rem;
		color: #100f0f;
		letter-spacing: -0.02em;
	}

	.hero-subtitle {
		font-size: 1.1rem;
		color: #5d5656;
		margin-bottom: 3.5rem;
		line-height: 1.6;
		max-width: 600px;
		margin-left: auto;
		margin-right: auto;
	}

	/* Contact Cards */
	.contact-cards {
		display: grid;
		grid-template-columns: 1fr;
		gap: 2rem;
	}

	@media (min-width: 768px) {
		.contact-cards {
			grid-template-columns: repeat(2, 1fr);
		}
	}

	.contact-card {
		background: #ffffff;
		border-radius: 12px;
		padding: 3rem 2rem;
		text-align: center;
		box-shadow:
			0 4px 6px -1px rgba(0, 0, 0, 0.05),
			0 2px 4px -1px rgba(0, 0, 0, 0.03);
		transition:
			transform 0.3s ease,
			box-shadow 0.3s ease;
		border: 1px solid rgba(0, 0, 0, 0.05);
	}

	.contact-card:hover {
		transform: translateY(-5px);
		box-shadow:
			0 10px 15px -3px rgba(0, 0, 0, 0.1),
			0 4px 6px -2px rgba(0, 0, 0, 0.05);
		border-color: #ff007f;
	}

	.contact-icon {
		width: 64px;
		height: 64px;
		background: #fae5e5;
		color: #ff007f;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		margin: 0 auto 1.5rem;
	}

	.contact-card h3 {
		font-size: 1.25rem;
		font-weight: 700;
		color: #100f0f;
		margin-top: 0;
		margin-bottom: 0.5rem;
	}

	.contact-card p {
		color: #5d5656;
		margin: 0;
		font-size: 1rem;
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
