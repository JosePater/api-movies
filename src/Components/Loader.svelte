<div class="lds-hourglass"></div>

<style>
    :root{
        --color1: #f70b0b;
        --color2: #314ef3;
        --width: 100px;
        --height: 100px;
    }

	.lds-hourglass {
		display: inline-block;
		position: relative;
		width: var(--width);
		height: var(--height);
	}
	.lds-hourglass:after {
		content: ' ';
		display: block;
		border-radius: 50%;
		width: var(--width);
		height: var(--height);
		margin: 8px;
		box-sizing: border-box;
		border: 50px solid #030303;
		border-color: var(--color1) transparent var(--color2) transparent;
		animation: lds-hourglass 1.2s infinite;
	}
	@keyframes lds-hourglass {
		0% {
			transform: rotate(0);
			animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
		}
		50% {
			transform: rotate(900deg);
			animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
		}
		100% {
			transform: rotate(1800deg);
		}
	}
</style>
