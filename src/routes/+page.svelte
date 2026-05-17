<script lang="ts">
	import { onMount } from 'svelte';
	let isLoaded = $state(false);

	let selectedOwnerNum = $state(0);
	let selectedTeacherNum = $state(0);
	let selectedStudentNum = $state(0);

	let ownerEmail = $derived(`owner${selectedOwnerNum}@email.com`);
	let teacherEmail = $derived(`teacher${selectedTeacherNum}@email.com`);
	let studentEmail = $derived(`student${selectedStudentNum}@email.com`);

	let copiedEmail = $state<string | null>(null);
	let copiedPassword = $state<string | null>(null);

	function copyToClipboard(text: string, type: 'email' | 'password', role: string) {
		navigator.clipboard.writeText(text);
		if (type === 'email') {
			copiedEmail = role;
			setTimeout(() => {
				if (copiedEmail === role) copiedEmail = null;
			}, 2000);
		} else {
			copiedPassword = role;
			setTimeout(() => {
				if (copiedPassword === role) copiedPassword = null;
			}, 2000);
		}
	}

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
			<a
				href="https://ta3alam.app/demo"
				target="_blank"
				rel="noopener noreferrer"
				class="btn-primary small-nav">Demo</a
			>
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
			<div class="cta-group">
				<a
					href="https://ta3alam.app/demo"
					target="_blank"
					rel="noopener noreferrer"
					class="btn-primary large"
				>
					Launch Demo
				</a>
				<a href="#demo" class="btn-secondary large"> View Credentials </a>
			</div>
		</div>
	</main>

	<section id="demo" class="demo-section">
		<div class="demo-container">
			<h2 class="demo-title">Try the Interactive Demo</h2>
			<p class="demo-subtitle">
				Experience the platform firsthand. Select an account, copy the credentials, and log in to
				explore each dashboard.
			</p>

			<div class="demo-grid">
				<!-- Owner Card -->
				<div class="demo-card">
					<div class="card-header">
						<div class="role-icon owner-bg">
							<svg
								xmlns="http://www.w3.org/2000/svg"
								viewBox="0 0 24 24"
								fill="currentColor"
								class="h-6 w-6"
							>
								<path d="M2 19h20v2H2v-2zm1-2h18L19.5 7 15 11l-3-6-3 6L4.5 7 3 17z" />
							</svg>
						</div>
						<div class="role-info">
							<h3>School Owner</h3>
							<span class="role-badge owner-badge">Administrator</span>
						</div>
					</div>
					<p class="role-desc">
						Manage school settings, departments, classrooms, teachers, and students. Oversee all
						platform activity.
					</p>

					<div class="selector-label">Select Account (0 - 5)</div>
					<div class="pill-group">
						{#each [0, 1, 2, 3, 4, 5] as num (num)}
							<button
								class="pill-btn"
								class:active={selectedOwnerNum === num}
								onclick={() => (selectedOwnerNum = num)}
							>
								{num}
							</button>
						{/each}
					</div>

					<div class="credential-box">
						<div class="credential-field">
							<span class="field-label">Email</span>
							<div class="field-value-container">
								<span class="field-value">{ownerEmail}</span>
								<button
									class="copy-btn"
									onclick={() => copyToClipboard(ownerEmail, 'email', 'owner')}
									aria-label="Copy Email"
								>
									{#if copiedEmail === 'owner'}
										<span class="copied-indicator">Copied!</span>
									{:else}
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="h-4 w-4"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M15.75 17.25v3.375c0 .621-.504 1.125-1.125 1.125h-9.75a1.125 1.125 0 0 1-1.125-1.125V7.875c0-.621.504-1.125 1.125-1.125H6.75a9.06 9.06 0 0 1 1.5.124m7.5 10.376A8.965 8.965 0 0 0 12 12.75c-.197 0-.39.024-.577.072m6.327 5.403A9.06 9.06 0 0 0 19.5 12c0-3.08-1.543-5.799-3.906-7.466M7.347 18.271A8.966 8.966 0 0 1 6.75 12.75c.197 0 .39-.024.577-.072m0 0a8.967 8.967 0 0 1 10.8 0m-10.8 0a8.969 8.969 0 0 1-1.428-1.78l1.78-1.78m0 0a8.967 8.967 0 0 1 6.58-6.58L12.75 6.75m0 0a8.97 8.97 0 0 1 1.78 1.428l-1.78 1.78"
											/>
										</svg>
									{/if}
								</button>
							</div>
						</div>

						<div class="credential-field">
							<span class="field-label">Password</span>
							<div class="field-value-container">
								<span class="field-value">password</span>
								<button
									class="copy-btn"
									onclick={() => copyToClipboard('password', 'password', 'owner')}
									aria-label="Copy Password"
								>
									{#if copiedPassword === 'owner'}
										<span class="copied-indicator">Copied!</span>
									{:else}
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="h-4 w-4"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M15.75 17.25v3.375c0 .621-.504 1.125-1.125 1.125h-9.75a1.125 1.125 0 0 1-1.125-1.125V7.875c0-.621.504-1.125 1.125-1.125H6.75a9.06 9.06 0 0 1 1.5.124m7.5 10.376A8.965 8.965 0 0 0 12 12.75c-.197 0-.39.024-.577.072m6.327 5.403A9.06 9.06 0 0 0 19.5 12c0-3.08-1.543-5.799-3.906-7.466M7.347 18.271A8.966 8.966 0 0 1 6.75 12.75c.197 0 .39-.024.577-.072m0 0a8.967 8.967 0 0 1 10.8 0m-10.8 0a8.969 8.969 0 0 1-1.428-1.78l1.78-1.78m0 0a8.967 8.967 0 0 1 6.58-6.58L12.75 6.75m0 0a8.97 8.97 0 0 1 1.78 1.428l-1.78 1.78"
											/>
										</svg>
									{/if}
								</button>
							</div>
						</div>
					</div>

					<a
						href="https://ta3alam.app/demo"
						target="_blank"
						rel="noopener noreferrer"
						class="btn-card-launch owner-btn"
					>
						Launch Owner Demo
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 20 20"
							fill="currentColor"
							class="ml-1 h-4 w-4"
						>
							<path
								fill-rule="evenodd"
								d="M3 10a.75.75 0 01.75-.75h10.638L10.23 5.29a.75.75 0 111.04-1.08l5.5 5.25a.75.75 0 010 1.08l-5.5 5.25a.75.75 0 11-1.04-1.08l4.158-3.96H3.75A.75.75 0 013 10z"
								clip-rule="evenodd"
							/>
						</svg>
					</a>
				</div>

				<!-- Teacher Card -->
				<div class="demo-card">
					<div class="card-header">
						<div class="role-icon teacher-bg">
							<svg
								xmlns="http://www.w3.org/2000/svg"
								viewBox="0 0 24 24"
								fill="currentColor"
								class="h-6 w-6"
							>
								<path
									d="M12 3L1 9l11 6 9-4.91V17h2V9L12 3zm0 13.5c-2.33 0-4.32-.93-5.78-2.44L12 18l5.78-3.94c-1.46 1.51-3.45 2.44-5.78 2.44z"
								/>
							</svg>
						</div>
						<div class="role-info">
							<h3>Teacher</h3>
							<span class="role-badge teacher-badge">Instructor</span>
						</div>
					</div>
					<p class="role-desc">
						Create and distribute lessons, design assignments (with audio recordings), grade
						submissions, and track progress.
					</p>

					<div class="selector-label">Select Account (0 - 5)</div>
					<div class="pill-group">
						{#each [0, 1, 2, 3, 4, 5] as num (num)}
							<button
								class="pill-btn"
								class:active={selectedTeacherNum === num}
								onclick={() => (selectedTeacherNum = num)}
							>
								{num}
							</button>
						{/each}
					</div>

					<div class="credential-box">
						<div class="credential-field">
							<span class="field-label">Email</span>
							<div class="field-value-container">
								<span class="field-value">{teacherEmail}</span>
								<button
									class="copy-btn"
									onclick={() => copyToClipboard(teacherEmail, 'email', 'teacher')}
									aria-label="Copy Email"
								>
									{#if copiedEmail === 'teacher'}
										<span class="copied-indicator">Copied!</span>
									{:else}
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="h-4 w-4"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M15.75 17.25v3.375c0 .621-.504 1.125-1.125 1.125h-9.75a1.125 1.125 0 0 1-1.125-1.125V7.875c0-.621.504-1.125 1.125-1.125H6.75a9.06 9.06 0 0 1 1.5.124m7.5 10.376A8.965 8.965 0 0 0 12 12.75c-.197 0-.39.024-.577.072m6.327 5.403A9.06 9.06 0 0 0 19.5 12c0-3.08-1.543-5.799-3.906-7.466M7.347 18.271A8.966 8.966 0 0 1 6.75 12.75c.197 0 .39-.024.577-.072m0 0a8.967 8.967 0 0 1 10.8 0m-10.8 0a8.969 8.969 0 0 1-1.428-1.78l1.78-1.78m0 0a8.967 8.967 0 0 1 6.58-6.58L12.75 6.75m0 0a8.97 8.97 0 0 1 1.78 1.428l-1.78 1.78"
											/>
										</svg>
									{/if}
								</button>
							</div>
						</div>

						<div class="credential-field">
							<span class="field-label">Password</span>
							<div class="field-value-container">
								<span class="field-value">password</span>
								<button
									class="copy-btn"
									onclick={() => copyToClipboard('password', 'password', 'teacher')}
									aria-label="Copy Password"
								>
									{#if copiedPassword === 'teacher'}
										<span class="copied-indicator">Copied!</span>
									{:else}
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="h-4 w-4"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M15.75 17.25v3.375c0 .621-.504 1.125-1.125 1.125h-9.75a1.125 1.125 0 0 1-1.125-1.125V7.875c0-.621.504-1.125 1.125-1.125H6.75a9.06 9.06 0 0 1 1.5.124m7.5 10.376A8.965 8.965 0 0 0 12 12.75c-.197 0-.39.024-.577.072m6.327 5.403A9.06 9.06 0 0 0 19.5 12c0-3.08-1.543-5.799-3.906-7.466M7.347 18.271A8.966 8.966 0 0 1 6.75 12.75c.197 0 .39-.024.577-.072m0 0a8.967 8.967 0 0 1 10.8 0m-10.8 0a8.969 8.969 0 0 1-1.428-1.78l1.78-1.78m0 0a8.967 8.967 0 0 1 6.58-6.58L12.75 6.75m0 0a8.97 8.97 0 0 1 1.78 1.428l-1.78 1.78"
											/>
										</svg>
									{/if}
								</button>
							</div>
						</div>
					</div>

					<a
						href="https://ta3alam.app/demo"
						target="_blank"
						rel="noopener noreferrer"
						class="btn-card-launch teacher-btn"
					>
						Launch Teacher Demo
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 20 20"
							fill="currentColor"
							class="ml-1 h-4 w-4"
						>
							<path
								fill-rule="evenodd"
								d="M3 10a.75.75 0 01.75-.75h10.638L10.23 5.29a.75.75 0 111.04-1.08l5.5 5.25a.75.75 0 010 1.08l-5.5 5.25a.75.75 0 11-1.04-1.08l4.158-3.96H3.75A.75.75 0 013 10z"
								clip-rule="evenodd"
							/>
						</svg>
					</a>
				</div>

				<!-- Student Card -->
				<div class="demo-card">
					<div class="card-header">
						<div class="role-icon student-bg">
							<svg
								xmlns="http://www.w3.org/2000/svg"
								viewBox="0 0 24 24"
								fill="currentColor"
								class="h-6 w-6"
							>
								<path
									d="M12 3a3 3 0 1 0 0 6 3 3 0 0 0 0-6zm-7 9.75v5.5a1.75 1.75 0 0 0 1.75 1.75h10.5a1.75 1.75 0 0 0 1.75-1.75v-5.5a2.75 2.75 0 0 0-2.75-2.75h-8.5a2.75 2.75 0 0 0-2.75 2.75z"
								/>
							</svg>
						</div>
						<div class="role-info">
							<h3>Student</h3>
							<span class="role-badge student-badge">Learner</span>
						</div>
					</div>
					<p class="role-desc">
						Access registered classes, view and download resources, submit assignments, and review
						grades.
					</p>

					<div class="selector-label">Select Account (0 - 5)</div>
					<div class="pill-group">
						{#each [0, 1, 2, 3, 4, 5] as num (num)}
							<button
								class="pill-btn"
								class:active={selectedStudentNum === num}
								onclick={() => (selectedStudentNum = num)}
							>
								{num}
							</button>
						{/each}
					</div>

					<div class="credential-box">
						<div class="credential-field">
							<span class="field-label">Email</span>
							<div class="field-value-container">
								<span class="field-value">{studentEmail}</span>
								<button
									class="copy-btn"
									onclick={() => copyToClipboard(studentEmail, 'email', 'student')}
									aria-label="Copy Email"
								>
									{#if copiedEmail === 'student'}
										<span class="copied-indicator">Copied!</span>
									{:else}
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="h-4 w-4"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M15.75 17.25v3.375c0 .621-.504 1.125-1.125 1.125h-9.75a1.125 1.125 0 0 1-1.125-1.125V7.875c0-.621.504-1.125 1.125-1.125H6.75a9.06 9.06 0 0 1 1.5.124m7.5 10.376A8.965 8.965 0 0 0 12 12.75c-.197 0-.39.024-.577.072m6.327 5.403A9.06 9.06 0 0 0 19.5 12c0-3.08-1.543-5.799-3.906-7.466M7.347 18.271A8.966 8.966 0 0 1 6.75 12.75c.197 0 .39-.024.577-.072m0 0a8.967 8.967 0 0 1 10.8 0m-10.8 0a8.969 8.969 0 0 1-1.428-1.78l1.78-1.78m0 0a8.967 8.967 0 0 1 6.58-6.58L12.75 6.75m0 0a8.97 8.97 0 0 1 1.78 1.428l-1.78 1.78"
											/>
										</svg>
									{/if}
								</button>
							</div>
						</div>

						<div class="credential-field">
							<span class="field-label">Password</span>
							<div class="field-value-container">
								<span class="field-value">password</span>
								<button
									class="copy-btn"
									onclick={() => copyToClipboard('password', 'password', 'student')}
									aria-label="Copy Password"
								>
									{#if copiedPassword === 'student'}
										<span class="copied-indicator">Copied!</span>
									{:else}
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewBox="0 0 24 24"
											stroke-width="1.5"
											stroke="currentColor"
											class="h-4 w-4"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												d="M15.75 17.25v3.375c0 .621-.504 1.125-1.125 1.125h-9.75a1.125 1.125 0 0 1-1.125-1.125V7.875c0-.621.504-1.125 1.125-1.125H6.75a9.06 9.06 0 0 1 1.5.124m7.5 10.376A8.965 8.965 0 0 0 12 12.75c-.197 0-.39.024-.577.072m6.327 5.403A9.06 9.06 0 0 0 19.5 12c0-3.08-1.543-5.799-3.906-7.466M7.347 18.271A8.966 8.966 0 0 1 6.75 12.75c.197 0 .39-.024.577-.072m0 0a8.967 8.967 0 0 1 10.8 0m-10.8 0a8.969 8.969 0 0 1-1.428-1.78l1.78-1.78m0 0a8.967 8.967 0 0 1 6.58-6.58L12.75 6.75m0 0a8.97 8.97 0 0 1 1.78 1.428l-1.78 1.78"
											/>
										</svg>
									{/if}
								</button>
							</div>
						</div>
					</div>

					<a
						href="https://ta3alam.app/demo"
						target="_blank"
						rel="noopener noreferrer"
						class="btn-card-launch student-btn"
					>
						Launch Student Demo
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 20 20"
							fill="currentColor"
							class="ml-1 h-4 w-4"
						>
							<path
								fill-rule="evenodd"
								d="M3 10a.75.75 0 01.75-.75h10.638L10.23 5.29a.75.75 0 111.04-1.08l5.5 5.25a.75.75 0 010 1.08l-5.5 5.25a.75.75 0 11-1.04-1.08l4.158-3.96H3.75A.75.75 0 013 10z"
								clip-rule="evenodd"
							/>
						</svg>
					</a>
				</div>
			</div>
		</div>
	</section>

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

	.btn-secondary {
		background: transparent;
		color: #100f0f;
		padding: 0.6rem 1.5rem;
		border-radius: 8px;
		font-weight: 600;
		font-size: 0.95rem;
		border: 2px solid #100f0f;
		transition: all 0.2s ease;
		display: inline-flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		margin-left: 1rem;
	}

	.btn-secondary:hover {
		transform: translateY(-2px);
		background: rgba(16, 15, 15, 0.05);
		box-shadow: 0 4px 12px rgba(16, 15, 15, 0.1);
	}

	.btn-secondary.large {
		padding: 0.8rem 2rem;
		font-size: 1.05rem;
	}

	.btn-primary.small-nav {
		padding: 0.4rem 1rem;
		font-size: 0.85rem;
		border-radius: 6px;
	}

	/* Demo Section */
	.demo-section {
		background-color: #e9e7e7;
		padding: 5rem 5%;
		border-top: 1px solid rgba(16, 15, 15, 0.08);
		border-bottom: 1px solid rgba(16, 15, 15, 0.08);
		width: 100%;
		display: flex;
		justify-content: center;
	}

	.demo-container {
		max-width: 1200px;
		width: 100%;
		text-align: center;
	}

	.demo-title {
		font-size: 2.25rem;
		font-weight: 800;
		color: #100f0f;
		margin-bottom: 0.75rem;
		letter-spacing: -0.01em;
	}

	.demo-subtitle {
		font-size: 1.1rem;
		color: #5d5656;
		margin-bottom: 3.5rem;
		max-width: 600px;
		margin-left: auto;
		margin-right: auto;
		line-height: 1.6;
	}

	.demo-grid {
		display: grid;
		grid-template-columns: 1fr;
		gap: 2.5rem;
	}

	@media (min-width: 1024px) {
		.demo-grid {
			grid-template-columns: repeat(3, 1fr);
		}
	}

	.demo-card {
		background: #ffffff;
		border-radius: 16px;
		padding: 2rem;
		box-shadow: 0 10px 30px rgba(0, 0, 0, 0.04);
		border: 1px solid rgba(16, 15, 15, 0.05);
		text-align: left;
		display: flex;
		flex-direction: column;
		transition:
			transform 0.3s cubic-bezier(0.16, 1, 0.3, 1),
			box-shadow 0.3s ease;
	}

	.demo-card:hover {
		transform: translateY(-8px);
		box-shadow: 0 20px 40px rgba(0, 0, 0, 0.08);
	}

	.card-header {
		display: flex;
		align-items: center;
		gap: 1rem;
		margin-bottom: 1.25rem;
	}

	.role-icon {
		width: 3.25rem;
		height: 3.25rem;
		border-radius: 12px;
		display: flex;
		align-items: center;
		justify-content: center;
		color: white;
	}

	.owner-bg {
		background: linear-gradient(135deg, #f59e0b, #d97706);
	}

	.teacher-bg {
		background: linear-gradient(135deg, #3b82f6, #2563eb);
	}

	.student-bg {
		background: linear-gradient(135deg, #10b981, #059669);
	}

	.role-info h3 {
		font-size: 1.2rem;
		font-weight: 700;
		color: #100f0f;
		margin: 0;
	}

	.role-badge {
		font-size: 0.75rem;
		font-weight: 600;
		padding: 0.15rem 0.5rem;
		border-radius: 6px;
		display: inline-block;
		margin-top: 0.25rem;
	}

	.owner-badge {
		background-color: #fef3c7;
		color: #b45309;
	}

	.teacher-badge {
		background-color: #dbeafe;
		color: #1d4ed8;
	}

	.student-badge {
		background-color: #d1fae5;
		color: #047857;
	}

	.role-desc {
		font-size: 0.925rem;
		color: #5d5656;
		line-height: 1.5;
		margin-top: 0;
		margin-bottom: 1.5rem;
		flex-grow: 1;
	}

	.selector-label {
		font-size: 0.8rem;
		font-weight: 600;
		color: #888;
		text-transform: uppercase;
		letter-spacing: 0.05em;
		margin-bottom: 0.5rem;
	}

	.pill-group {
		display: flex;
		gap: 0.35rem;
		margin-bottom: 1.5rem;
		background: #f3f2f2;
		padding: 0.25rem;
		border-radius: 10px;
	}

	.pill-btn {
		flex: 1;
		background: transparent;
		border: none;
		padding: 0.4rem 0;
		font-size: 0.9rem;
		font-weight: 600;
		color: #5d5656;
		border-radius: 7px;
		cursor: pointer;
		transition: all 0.2s ease;
	}

	.pill-btn:hover {
		color: #100f0f;
		background-color: rgba(0, 0, 0, 0.03);
	}

	.pill-btn.active {
		background: white;
		color: #100f0f;
		box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
	}

	.credential-box {
		background: #f7f6f6;
		border-radius: 12px;
		padding: 1rem;
		margin-bottom: 1.5rem;
		border: 1px solid rgba(0, 0, 0, 0.02);
	}

	.credential-field {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
	}

	.credential-field:not(:last-child) {
		margin-bottom: 0.75rem;
		border-bottom: 1px solid rgba(16, 15, 15, 0.06);
		padding-bottom: 0.75rem;
	}

	.field-label {
		font-size: 0.75rem;
		font-weight: 500;
		color: #888;
	}

	.field-value-container {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 1rem;
	}

	.field-value {
		font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
		font-size: 0.875rem;
		color: #100f0f;
		font-weight: 600;
		word-break: break-all;
	}

	.copy-btn {
		background: transparent;
		border: none;
		color: #ff007f;
		padding: 0.25rem;
		border-radius: 6px;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: all 0.2s ease;
	}

	.copy-btn:hover {
		background-color: rgba(255, 0, 127, 0.08);
		transform: scale(1.05);
	}

	.copied-indicator {
		font-size: 0.75rem;
		font-weight: 700;
		color: #047857;
		background-color: #d1fae5;
		padding: 0.1rem 0.4rem;
		border-radius: 4px;
		animation: pulse 1s infinite alternate;
	}

	@keyframes pulse {
		from {
			opacity: 0.8;
		}
		to {
			opacity: 1;
		}
	}

	.btn-card-launch {
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 0.75rem 1rem;
		border-radius: 10px;
		font-weight: 700;
		font-size: 0.95rem;
		text-align: center;
		transition: all 0.2s ease;
		color: white;
		box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
	}

	.btn-card-launch:hover {
		transform: translateY(-2px);
		box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
	}

	.owner-btn {
		background: #d97706;
	}
	.owner-btn:hover {
		background: #b45309;
	}

	.teacher-btn {
		background: #2563eb;
	}
	.teacher-btn:hover {
		background: #1d4ed8;
	}

	.student-btn {
		background: #059669;
	}
	.student-btn:hover {
		background: #047857;
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
