<script>
import {Configuration,OpenAIApi} from "openai";
import logo from "$lib/images/logo2.png"
let is_loading;
let res
let prompt = '';
const config=new Configuration({apiKey:"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"});
const api=new OpenAIApi(config);
const image = async () => {
	is_loading=true;
	res=await api.createImage({
		prompt: prompt,
		n:1,
		size:"512x512",
	})
	is_loading=false;
	console.log(res);
}
	function scrollToSection() {
		const element = document.getElementById('image-section');
		element.scrollIntoView({ behavior: 'smooth' });
	}
function handle_submit() {
	scrollToSection()
	image();
}

</script>
<div class="nav-div">

</div>
<section style="height: 100vh">
	<nav>
		<div class='logo lg:w-1/12 sm:w-1/6'>
			<a href="/"> <img src={logo} alt="logo" /></a>
		</div>
	</nav>
	<div class="main">
		<textarea bind:value={prompt} class="md:text-5xl sm:text-4xl outline-0 text-center" type="text" placeholder="Lets create something.."></textarea>
		<a href="#image-section"><button on:click={handle_submit} class="text-left btn">generate now 👌</button></a>
	</div>
</section>

<section id="image-section">
	{#if is_loading}
		<div class="main2">
			<iframe src="https://giphy.com/embed/l3nWhI38IWDofyDrW" width="480" height="480"></iframe>
		</div>
	{:else}
		{#if res}
			<div class="main2">
				<img src={res.data.data[0].url} alt="generated image">
			</div>
		{/if}
	{/if}
</section>
<style>
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
	.main {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		font-family: 'Roboto Mono', monospace;
		height: 70vh;
	}
	.main2{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		font-family: 'Roboto Mono', monospace;
		height: 100vh;
	}
	textarea{
		width: 100%;
		padding: 60px;
		text-wrap: normal;
	}
	.btn{
		background-color: #222222;
		color:white;
		padding: 10px;
		display: block;
		margin: 20px auto;
		border-radius: 10px;
	}
	@media (max-width:640px)  {
		.logo{
			width: 30.666667%;
		}
	}
</style>
