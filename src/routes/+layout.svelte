<script lang="ts">
	import '@fontsource-variable/inter';
	import '../app.css';
</script>

<div id="root" class="root">
	<header class="header">
		<button class="button">
			<span>&quest;</span>
		</button>
	</header>
	<slot />
	<footer class="footer">
		<div>
			Made by
			<a
				href="https://matovius.pages.dev"
				target="_blank"
				rel="noopener noreferrer"
				class="footer-link"
			>
				<svg class="icon" viewBox="0 0 500 500" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path
						d="M358.823 154.289L486.702 282.075C515.11 310.462 494.99 359 454.815 359H45.0945C20.1895 359 -0.00012207 338.825 -0.00012207 313.938V186.152C-0.00012207 146.006 48.5732 125.901 76.9812 154.289L204.86 282.075C233.268 310.462 281.842 290.357 281.842 250.211V186.152C281.842 146.006 330.415 125.901 358.823 154.289Z"
						fill="currentColor"
					/>
				</svg>
			</a>
		</div>
	</footer>
</div>

<style>
	.root {
		width: 100dvw;
		height: 100dvh;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	header,
	footer {
		width: 100%;
		display: flex;
		flex-direction: row;
		padding: 12px;
		position: fixed;
	}

	header {
		top: 0;

		justify-content: flex-end;
		align-items: center;
	}

	footer {
		bottom: 0;

		justify-content: center;
		align-items: center;

		& > div {
			display: flex;
			flex-direction: row;
			gap: 8px;

			@media (prefers-color-scheme: light) {
				color: hsl(0, 0%, 0%, 0.6);
			}

			@media (prefers-color-scheme: dark) {
				color: hsl(0, 0%, 100%, 0.6);
			}
		}
	}

	a.footer-link {
		color: inherit;
		outline: 2px solid transparent;
		outline-offset: 2px;

		@media (prefers-color-scheme: light) {
			&:hover,
			&:focus {
				color: hsl(0, 0%, 0%);
			}

			&:focus-visible {
				outline-color: hsl(0, 0%, 0%, 0.6);
			}
		}

		@media (prefers-color-scheme: dark) {
			&:hover,
			&:focus {
				color: hsl(0, 0%, 100%);
			}

			&:focus-visible {
				outline-color: hsl(0, 0%, 100%, 0.6);
			}
		}

		& > .icon {
			width: 24px;
			height: 24px;
			aspect-ratio: 1;
		}
	}

	button.button {
		color: hsl(0, 0%, 100%);
		font-weight: 600;
		padding: 8px 16px;
		border-radius: 9999rem;
		border: none;
		background: transparent;
		cursor: pointer;
		outline: 2px solid transparent;

		@media (prefers-color-scheme: light) {
			color: hsl(0, 0%, 0%);

			&:hover,
			&:focus {
				background: hsl(0, 0%, 0%, 0.2);
			}

			&:focus-visible {
				outline-color: hsl(0, 0%, 0%);
			}
		}

		@media (prefers-color-scheme: dark) {
			color: hsl(0, 0%, 100%);

			&:hover,
			&:focus {
				background: hsl(0, 0%, 100%, 0.2);
			}

			&:focus-visible {
				outline-color: hsl(0, 0%, 100%);
			}
		}
	}
</style>
