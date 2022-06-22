<script lang="ts">
	
	import InfoAboutMe from "./components/infoAboutMe.svelte";
	import Header from "./components/header.svelte";
	import Weather from "./components/weather.svelte"
	import Footer from "./components/footer.svelte";

	let condition: number = 1;
	function buttonCount() {
		condition += 1;
	}

</script>

<main>

	<Header {condition}>
		<div id="nav" class="nav_links">
			<a href="#text" on:click={buttonCount} id="btn" class="link_to_page">
				{condition % 2 === 1 ? 'Check weather' : 'Return to the main page'}
			</a>
		</div>
	</Header>

	{#if condition % 2 === 1} 
		<InfoAboutMe />
	{:else}
		<Weather />
	{/if}
	
	<Footer />

</main>

<style>

	.link_to_page {
        color: #6c757d;
        background: linear-gradient(45deg, #6f42c1, #DDEC6A);
        border: 0;
        font-family: serif;
        cursor: pointer;
        font-size: 25px;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        text-decoration: none;
        margin-right: 20px;
        opacity: 0.4;
        transition: 0.2s linear;
    }

    .link_to_page:hover {
        opacity: 1;

    }
	
	.nav_links {
        margin-top: 0;
        background: #212529;
        padding-top: 20px;
        z-index: 1000;
        padding-left: 40px;
        width: 100%;
        height: 50px;
		position: fixed;
        left: 0;
        top: 0;
    }

	@media (max-width: 720px) {

		.nav_links {
			font-size: 15px;
			height: 35px;
		}

		.link_to_page {
			font-size: 15px;
		}
	}


	@media (max-width: 540px) {
		.nav_links {
			padding-right: 0;
		}
	}

</style>