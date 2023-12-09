<script>
	let sujet = '';
	let notice = '';
	let aides = '';
	let texteFinal = '';
	let texteArea;

	$: if (texteArea) {
		texteArea.style.height = 'auto'; // Réinitialiser la hauteur
		texteArea.style.height = texteArea.scrollHeight + 'px'; // Ajuster à la hauteur du contenu
	}
  
	function genererTexte() {
	  texteFinal = `Rédiges moi une notice pour le sujet suivant : ${sujet}\n\nVoilà les éléments de la notice : ${notice}\n\nLes conseils disponibles sont les suivants : ${aides}.<br>Le texte est à destination des néophytes.<br>Il doit être raisonnablement chaleureux.<br>Il doit y avoir une introduction.<br>Tu dois favoriser l’utilisation de listes`;
	}

	function copierTexte() {
    navigator.clipboard.writeText(texteFinal).then(() => {
      // Vous pouvez ajouter ici un message de confirmation ou une action après la copie
      console.log('Texte copié avec succès!');
    });
  	}
  </script>
  
  <style>

	.app-container {
    background-color: #E7DDCE; /* Couleur de fond pour le conteneur de l'application */
  	}

	input {
	  margin-bottom: 10px;
	  width: 100%;
	  padding: 8px;
	  background-color: white;
	  border-radius: 8px;
	}
	textarea {
	  margin-bottom: 10px;
	  width: 100%;
	  padding: 8px;
	  height: auto;
	  background-color: white;
	  border-radius: 8px;
	  min-height: 200px; /* Hauteur minimale initiale */
      overflow-y: hidden;
	}


	button {
    background-color: #188803; /* Couleur de fond du bouton */
    color: white; /* Couleur du texte du bouton */
    border: 2px solid #188803; /* Bordure du bouton */
    border-radius: 8px; /* Rayon de la bordure du bouton */
    padding: 10px 15px;
    cursor: pointer;
    transition: background-color 0.3s; /* Effet de transition pour le survol */
 	}

	button svg {
	margin-right: 5px; /* Espace entre l'icône et le texte */
	}

	.input {
	  min-height: 50px;
	  height: auto;
	}
  </style>
  
  <body>
	<div class="app-container">
		<h2>Enki Prompt Generator</h2>
		<input type="text" bind:value={sujet} placeholder="Sujet" />
		<textarea bind:value={notice} placeholder="Notice" rows="4" class="input"></textarea>
		<textarea bind:value={aides} placeholder="Aides" rows="4" class="input"></textarea>
		<button on:click={genererTexte}>Générer</button>
		<div>
			<h3>Texte Généré</h3>
			<textarea readonly bind:this={texteArea}>{texteFinal}</textarea>
			<button on:click={copierTexte}>
			  <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-clipboard" viewBox="0 0 16 16">
				<path d="M10.5 1.5A.5.5 0 0 1 11 2v1h1.5a.5.5 0 0 1 .5.5V4h-1v3a.5.5 0 0 1-1 0V4H9v-.5a.5.5 0 0 1 .5-.5H10V2a.5.5 0 0 1 .5-.5zM9.5 2a.5.5 0 0 1-.5.5V4h-1v-.5a.5.5 0 0 1-.5-.5V2a.5.5 0 0 1 .5-.5zM6 4H2.5A.5.5 0 0 1 2 3.5v9c0 .825.675 1.5 1.5 1.5H6V4z"/>
				<path d="M2.5 1a.5.5 0 0 1 .5.5V3h9V1.5a.5.5 0 0 1 .5-.5h1a.5.5 0 0 1 .5.5v1h-1V3H2v-.5a.5.5 0 0 1-.5-.5H1a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h1z"/>
			  </svg>
			  Copier le prompt
			</button>
		  </div>
	  </div>
  </body>
 
  
  