<script>
	import {onMount} from 'svelte';
	import Plyr from 'plyr';

	let player;

	onMount(async()=>{
		player = new Plyr('#player');
	})


	const videos = [
		{ title: "coKPIt", src: "ABDESLAM-AGZOUL", names: "Abdeslam AGZOUL", dpt: "Opérations SEA"},
		{ title: "Rations de combat", src: "ALAIN-MUDERS", names: "Alain MUDERS", dpt: "Opérations SEA"},
		{ title: "Charte RED", src: "BENOIT-LUC", names: "Benoit LUC", dpt: "Département RSE"},
		{ title: "SIAR activité non aérienne", src: "CHRISTIAN-JOSSE", names: "Christian JOSSE", dpt: "Développement des Nouveaux Marchés"},
		{ title: "Maitriser la matière MMAT", src: "DANIELA-RAMIREZ", names: "Daniela RAMIREZ", dpt: "Process Industriels"},
		{ title: "Les Collections Culiniares Servair", src: "DELPHINE-DISTEFANO", names: "Delphine DI STEFANO", dpt: "Développement des Nouveaux Marchés"},
		{ title: "Vols Test Delta Airline", src: "ERONCI-STHUEUX", names: "Emanuela RONCI,<br> Stéphanie THUEUX", dpt: "Département Commercial"},
		{ title: "PAC Long Courrier", src: "HERVE-BOURGAIN", names: "Hervé BOURGAIN", dpt: "Opérations SEA"},
		{ title: "Projet gategroup de centrale d'achats", src: "HUGO-SOUCHET", names: "Hugo SOUCHET", dpt: "Département Achats"},
		{ title: "Appel d'offre Passerelle CDG", src: "JULIEN-VASSEL", names: "Julien VASSEL", dpt: "Opérations SEA"},
		{ title: "La nutrition chez Servair", src: "LAURA-SCAGNI", names: "Laura SCAGNI", dpt: "Département R&D"},
		{ title: "Sacs Prodige", src: "LAURENT-CHASSAGNEVIROL", names: "Laurent CHASSAGNEVIROL", dpt: "Département R&D"},
		{ title: "Déploiement de Xops (Panda)", src: "MAXENCE-DUPLAND", names: "Maxence DUPLAND", dpt: "Process Industriels"},
		{ title: "Organisation Commerciale et Opérationnelle", src: "MICHEL-PIERLOVSKI", names: "Michel PIERLOVISI", dpt: "Commercial"},
		{ title: "Projet MESO", src: "ROGER-ABIJABER", names: "Roger ABI-JABER", dpt: "Opérations SEA"},
		{ title: "Passage de l'activité été 2021", src: "SOFIANE-DAHAK", names: "Sofiane DAHAK", dpt: "Opérations SEA"},
		{ title: "Cocooning et nouveau contrat TCR", src: "YANN-COLLET", names: "Yann COLLET", dpt: "Servlogistic"},
	]
	let currentSource = videos[0].src

	let changeSource = (v) => {
		console.log("hop")
		player.source = {
		type: 'video',
		title: v.title,
		sources: [
			{
				src: `/videos/${v.src}.mp4`,
				type: 'video/mp4'
				//size: 720,
			} 
		],
		poster: `/videos/${v.src}.jpg`
	};
	window.scroll(0,0);
	player.play();
}

</script>

<main>
	<!-- svelte-ignore a11y-media-has-caption -->
	<section class="grid_wrapper">
		<div class="column"/>
		<div class="column">
			<img src="logo-servair.png">
			<p class="subtitre"><strong>Réunions de l'encadrement - Septembre 2021</strong></p>
		</div>
		<div class="column"/>
		
	</section>
	<!-- svelte-ignore a11y-media-has-caption -->
	<video id="player" playsinline controls data-poster="/videos/{currentSource}.jpg">
		<source src="/videos/{currentSource}.mp4" type="video/mp4" />
	</video>

	<section class="grid_wrapper">
		{#each videos as v}
		  <div class="column" on:click={()=>changeSource(v)}>
			<div class="image-wrapper">
				<div class="media">
					<div class="overlay"></div>
					<img src="/videos/{v.src}.jpg" alt="{v.title}">
					<div class="under">{v.title}</div>
					<div class="image-details">
						<p style="margin-top:-6px;">
							{@html v.names}<br>
							<span style="font-weight:100">{v.dpt}</span>
						</p>
					</div>
				</div>
			</div>
		  </div>
		  {/each}
		</section>

	
	
</main>

<style>
	
@import url('https://fonts.googleapis.com/css2?family=Jost:wght@100;300;400;700&display=swap');


.image-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 98%;
  border: 1px royalblue solid;
  border-radius: 4px;
  margin-block-start: 10px;
}

.media {
  width: auto;
  height: fill-available;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 10px;
  overflow: hidden;
  position: relative;
}

.media:hover {
  cursor: pointer;
}

.overlay {
  background: rgba(0, 0, 0, 0.7);
  position: absolute;
  height: 100%;
  width: 100%;
  z-index: 3;
  opacity: 0;
  overflow: clip;
  transition: all ease-in-out 0.5s;
}

.media:hover .overlay {
  opacity: 1;
}

img {
  width: 100%;
  z-index: -1;
  margin: auto;
  transform: scale(1);
  transition: all ease-in-out 0.5s;
}

.under {
	padding-top:10px;
}

.media:hover img {
  transform: scale(1.1);
  filter: blur(2px);
}

.image-details {
  text-align: center;
  color: white;
  font-size: 20px;
  z-index: 4;
  position: absolute;
  top: 100%;
  opacity: 0;
  transition: all ease-in-out 0.5s;
}

.media:hover .image-details {
  top: 40%;
  opacity: 1;
}

:global(html) {
  box-sizing: border-box;
}

*, *:before, *:after {
  box-sizing: inherit;
}

main {
  max-width: 1200px;
  margin: 0 auto;
}

main .subtitre {
	margin-bottom:35px;
}
main h1 {
  margin: 20px 0;
}

.grid_wrapper {
  max-width: 1200px;
  margin: 0 auto;
  margin-top:30px;
}

@media (min-width: 768px) {
  .grid_wrapper {
    display: flex;
    flex-flow: row wrap;
  }
}

@media only screen and (max-width: 900px) {
  .media {
    width: 70%;
    height: 70%;
  }
}
.grid_wrapper .column {  
  flex-basis: 33.333%;
}


</style>