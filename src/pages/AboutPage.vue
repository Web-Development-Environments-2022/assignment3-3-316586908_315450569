<template>
<!-- <div>
    <h5>AboutPage</h5>
</div> -->
  <div>
   <div id="about_page" class="aboutClass" >
			<div class="aboutClass-inner">
				<center>
				<h1 class="headline">About Us Game</h1>
				</center>
				<div class="aboutSec">
					<h2 style="font-style:italic;">Pacman game</h2>
					<p id="about_para">
						The user can play and change the settings of number monsters, ball color, time and more as you wish.<br>
						We encountered difficulties such as html's design issues and some functionality of the game - it took us quite some time, but The assignment 1 of building a simple site helped us to meet the goals we set for ourselves.
						<br> used jQUERY to set functionalities such as identify details of new users to the game, set attributes dynamically to html elements, check values of elements and more...
						in addition, We used the regex expression to make sure the fields at the registration page were entered correctly.<br>
					</p>
				</div>
				<h1 id="contact" class="headline" style="text-align:center">Contact Our Team</h1>

				<div class="div0">
					<div class="div1">
						<div class="div2">
							<img id="tal" src="../images/tal.jpeg" alt="tal" >
							<div class="div3">
								<center>
							<h2>Tal Ben Hamou</h2>
							<p class="id">315450569</p>
							<p>Tal 27 years old, a third year student.</p>
							<p>tal.ben.hamou@post.bgu.ac.il</p>
							<div class="socialLogo">
								<a href="	https://www.instagram.com/tal.ben.hamo/">
								<img class="socialMedia" src="../images/instaLogo.png" alt="Instagram">
								</a>
							
								<a href="https://www.facebook.com/tal.benhamou.71">
								<img class="socialMedia" src="../images/facebookLogo.png" alt="Facebook">
								</a>
						
							</div>
							</center>
							</div>
						</div>
					</div>
				
					<div class="div1">
						<div class="div2">
							<img id="ido" src="../images/ido.jpeg" alt="ido">
							<div class="div3">
							<center>
							<h2>Ido Cohen</h2>
							<p class="id">316586908</p>
							<p>Ido 26 years old, a third year student.</p>
							<p>ido3@post.bgu.ac.il</p>
							<div class="socialLogo">
								<a href="https://www.instagram.com/idocohen32/">
								<img class="socialMedia" src="../images/instaLogo.png" alt="Instagram">
								</a>
							
								<a href="https://www.facebook.com/ido.cohen.560">
								<img class="socialMedia" src="../images/facebookLogo.png" alt="Facebook">
								</a>
						
							</div>

							</center>
							</div>
						</div>
					</div>
				</div>
            </div>
   </div>
  </div>
</template>

<script>
export default {
    name: "about"
}
</script>

<style>

.div0 {
    background-color: #232323;
    display: flex;
	justify-content: center;
}

.div1 {
    float: left;
    width: 48%;
    margin-bottom: 16px;
    padding: 11px;
}

.div2 {
    box-shadow: 0px 8px 10px 3px rgba(255, 255, 255, 0.2);
    margin: 4px;
}


.aboutSec {
    padding: 55px;
    text-align: center;
    background-color: #232323;
    color: white;
}

.div3 {
    padding: 0 10px;
    color: aliceblue;
    background-color: #232323;
}

.div3::after, .row::after {
    content: "";
    clear: both;
    display: table;
}

.id {
    color: rgb(114, 144, 176);
}

#ido, #tal {
    float: left;
    width:  665px;
    height: 600px;
    max-width: 100%;
    max-height: 100%;
    object-fit: cover;
    overflow: auto;
    display: inline;
    margin: 0 auto;
}

.headline{
    color: rgb(255, 79, 79);
}
/* 
#about_page{
    display: none;  
    position: fixed;  
    z-index: 3;  
    padding-top: 10px;  

    width: 100%; 
    height: 100%; 
    max-width: 100%;
    max-height: 100%;
    overflow: auto; 
    background-color: rgb(243, 243, 243); 
    background-color: rgba(56, 145, 97, 0.4); 
}  */

.aboutClass-inner {
    position: relative;
    margin: auto;
    border: 0px solid #888;
    width: 100%;
    max-width: 100%;
  }

      
#about_para{
    font-family:Arial, Helvetica, sans-serif;
    font: bold;
    font-size: larger;

}
</style>