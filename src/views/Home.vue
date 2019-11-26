<template>
	<div>
		<nav class="navbar is-fixed-top has-background-one" role="navigation">
			<div class="navbar-brand">
				<a
					role="button"
					class="navbar-burger burger"
					:class="{'is-active': burgerActive}"
					@click="burgerClicked"
				>
					<span aria-hidden="true"></span>
					<span aria-hidden="true"></span>
					<span aria-hidden="true"></span>
				</a>
			</div>

			<div
				class="navbar-menu"
				:class="{'is-active': burgerActive, 'has-background-one': !burgerActive, 'has-background-white': burgerActive }"
				:style="!burgerActive ? {marginLeft: windowWidth * 8 / 1920 + 'rem', marginRight: windowWidth * 8 / 1920 + 'rem'} : {}"
				@click="burgerClicked && windowWidth < 600"
			>
				<div class="navbar-start">
					<div class="navbar-item">
						<a
							class="navbar-item"
							:class="!burgerActive ? 'has-text-white' : ''"
							v-scroll-to="'#about'"
							@click="burgerActive = false"
						>About me</a>
						<a
							class="navbar-item"
							:class="!burgerActive ? 'has-text-white' : ''"
							v-scroll-to="'#skills'"
							@click="burgerActive = false"
						>Skills</a>
						<a
							class="navbar-item"
							:class="!burgerActive ? 'has-text-white' : ''"
							v-scroll-to="'#projects'"
							@click="burgerActive = false"
						>Projects</a>
					</div>
				</div>
				<div class="navbar-end">
					<div class="navbar-item">
						<a class="button is-four" v-scroll-to="'#contact'">Talk to me</a>
					</div>
				</div>
			</div>
		</nav>
		<section id="header" class="hero is-fullheight is-one">
			<div class="hero-body">
				<div class="container">
					<h4 class="subtitle">
						Hello
						<span>
							<strike>world</strike>
						</span>! I'm
					</h4>
					<h1 class="title">Gustavo Vasconcelos</h1>
					<h2 class="subtitle">Full-stack developer</h2>
				</div>
			</div>
		</section>
		<section id="about" class="section has-background-three">
			<div class="container">
				<h1 class="title has-text-white">About me</h1>
				<hr />
				<div class="columns">
					<div class="column is-centered is-4" data-aos="fade-right">
						<div>
							<img class="is-rounded" src="../assets/img/me.jpg" />
						</div>
						<span class="columns is-centered" style="font-size: 50px; margin-top: 5px;">
							<a href="https://linkedin.com/in/gustavo-vasconcelos" target="_blank">
								<i class="column fab fa-linkedin has-text-right button-hover"></i>
							</a>
							<a href="https://github.com/gustavo-vasconcelos" target="_blank">
								<i class="column fab fa-github-square has-text-right button-hover"></i>
							</a>
						</span>
					</div>

					<div class="column is-centered has-text-justified has-text-white" data-aos="fade-left">
						<p>
							I'm a
							<b>student</b> currently attending the 3rd grade of the undergraduate degree in Web Information Systems and Technologies at
							<a
								href="http://esmad.ipp.pt"
								target="_blank"
								class="has-text-white"
							>ESMAD (P.PORTO)</a>.
						</p>
						<br />
						<p>I find the web development and IT field very fascinating and interesting, as we use applications and services developed with these technologies on our daily basis.</p>
						<br />
						<p>During this 2 and a half years, I've been developing many projects under my academic studies, that I'm very proud of.</p>
						<br />
						<p>I'm proficient in both front and back end areas, but I mostly like back-end.</p>
					</div>
				</div>
			</div>
		</section>
		<section id="skills" class="section has-background-white">
			<div class="container">
				<h1 class="title has-text-black">Skills</h1>
				<hr class="has-background-black" />
				<div class="columns is-mobile is-multiline">
					<div
						class="column is-2-widescreen is-3-tablet is-4-mobile"
						v-for="(skill, index) in skills"
						:key="'skill_' + index"
						data-aos="fade-in"
					>
						<a :href="skill.linkInfo" target="_blank">
							<img :src="require(`@/assets/img/skills/${skill.img}`)" />
						</a>
					</div>
				</div>
			</div>
		</section>
		<section id="projects" class="section has-background-three">
			<div class="container">
				<h1 class="title has-text-white">Projects</h1>
				<hr />
				<div class="columns is-multiline">
					<div
						class="column is-4-widescreen is-6-tablet"
						v-for="(project, index) in projects"
						:key="'project_' + index"
						data-aos="fade-in"
					>
						<div class="card">
							<div class="card-content" @click="openModal(project)">
								<p class="is-size-4">{{ project.title }}</p>
							</div>
							<div class="card-image" @click="openModal(project)">
								<figure class="image">
									<img
										:src="require(`@/assets/img/projects/${project.title.toLowerCase().replace(/ /g, '')}/thumb.jpg`)"
										alt
									/>
								</figure>
							</div>

							<footer class="card-footer">
								<p class="card-footer-item" v-if="project.url.repository">
									<span>
										<a :href="project.url.repository" target="_blank" class="has-text-three">GitHub</a>
									</span>
								</p>
								<p class="card-footer-item" v-if="project.url.demo">
									<span>
										<a :href="project.url.demo" target="_blank" class="has-text-three">Live demo</a>
									</span>
								</p>
								<p class="card-footer-item">
									<span class="has-text-three" @click="openModal(project)">More info</span>
								</p>
							</footer>
						</div>
					</div>
				</div>
			</div>
		</section>
		<div class="modal" :class="{'is-active': modal.active}" v-if="modal.active">
			<div class="modal-background" @click="closeModal" data-aos="fade-in"></div>
			<div class="modal-card" data-aos="fade-up">
				<header class="modal-card-head">
					<p class="modal-card-title">{{ modal.project.title }}</p>
					<button class="delete" aria-label="close" @click="closeModal"></button>
				</header>
				<section class="modal-card-body has-text-left">
					<img
						v-if="modal.active"
						:src="require(`../assets/img/projects/${modal.project.title.toLowerCase().replace(/ /g, '')}/thumb.jpg`)"
						alt
					/>
					<div class="content">
						<div>
							<p class="is-size-5">Description</p>
							{{ modal.project.description }}
						</div>
						<div>
							<p class="is-size-5">Technologies</p>
							<ul>
								<li
									v-for="(technology, index) in modal.project.technologies"
									:key="'technology_' + index"
								>{{ technology }}</li>
							</ul>
						</div>
						<div v-if="modal.project.features">
							<p class="is-size-5">Main features</p>
							<ul>
								<template v-for="(feature, index) in modal.project.features">
									<li v-if="feature[0].length === 1" :key="'feature_' + index">{{ feature }}</li>
									<li :key="'feature_' + index" v-else>
										{{ feature[0] }}
										<ul>
											<template v-for="(subfeature, subIndex) in feature">
												<li v-if="subIndex > 0" :key="'subfeature_' + subIndex">{{ subfeature }}</li>
											</template>
										</ul>
									</li>
								</template>
							</ul>
						</div>
						<div>
							<p class="is-size-5">Screenshots:</p>
							<flickity class="flickity" ref="flickity" :options="flickityOptions">
								<div class="carousel-cell">
									<img src="https://i.pinimg.com/originals/6c/db/4b/6cdb4bfe644c483c97ba978b979c6a14.jpg" alt />
								</div>
								<div class="carousel-cell">
									<img src="http://getwallpapers.com/wallpaper/full/9/b/e/101097.jpg" alt />
								</div>
								<div class="carousel-cell">
									<img src="https://cdn.hipwallpaper.com/i/60/62/mtqL30.jpg" alt />
								</div>
								<div class="carousel-cell">
									<img src="https://wallpaperplay.com/walls/full/8/f/e/98382.jpg" alt />
								</div>
							</flickity>
						</div>
					</div>
				</section>
			</div>
		</div>

		<section id="contact" class="section">
			<div class="container">
				<h1 class="title">Talk to me</h1>
				<hr class="has-background-black" />
				<div class="columns is-centered has-text-left is-multiline">
					<div class="column is-6">
						<div
							class="notification is-primary"
							v-if="form.notification"
							@click="form.notification = false"
							data-aos="fade"
						>Your message was sent. I'll reply you ASAP.</div>
						<form @submit.prevent="sendEmail">
							<div class="field">
								<label class="label" for="email">Your email</label>
								<div class="control">
									<input id="email" class="input" type="email" v-model="form.data.email" required />
								</div>
							</div>
							<div class="field">
								<label class="label" for="subject">Subject</label>
								<div class="control">
									<input id="subject" class="input" type="text" v-model="form.data.subject" required />
								</div>
							</div>
							<div class="field">
								<label class="label" for="message">Message</label>
								<div class="control">
									<textarea
										id="message"
										class="textarea"
										name="message"
										v-model="form.data.message"
										required
									></textarea>
								</div>
							</div>
							<button
								type="submit"
								class="button is-two is-fullwidth"
								:class="{'is-loading': form.sending}"
							>Send</button>
						</form>
					</div>
				</div>
			</div>
		</section>
		<footer id="footer" class="has-background-two has-text-centered has-text-white">Me &copy; 2019</footer>
	</div>
</template>

<script>
import AOS from "aos"
import axios from "axios"
import Flickity from "vue-flickity"

export default {
	name: "home",
	components: { Flickity },
	data() {
		return {
			windowWidth: 0,
			burgerActive: false,
			skills: [
				{
					img: "html.png",
					linkInfo: "https://developer.mozilla.org/en-US/docs/Glossary/HTML"
				},
				{
					img: "css.png",
					linkInfo: "https://developer.mozilla.org/en-US/docs/Glossary/CSS"
				},
				{
					img: "js.png",
					linkInfo: "https://developer.mozilla.org/en-US/docs/Web/JavaScript"
				},
				{ img: "bootstrap.png", linkInfo: "https://getbootstrap.com/" },
				{ img: "bulma.png", linkInfo: "https://bulma.io/" },
				{ img: "vue.png", linkInfo: "https://vuejs.org/" },
				{ img: "npm.png", linkInfo: "https://www.npmjs.com/" },
				{ img: "node.png", linkInfo: "https://nodejs.org/" },
				{ img: "express.png", linkInfo: "https://expressjs.com/" },
				{ img: "mongo.png", linkInfo: "https://www.mongodb.com/" },
				{ img: "mysql.jpg", linkInfo: "https://www.mysql.com/" },
				{ img: "git.png", linkInfo: "https://git-scm.com/" },
				{ img: "three.png", linkInfo: "https://threejs.org/" },
				{ img: "arduino.png", linkInfo: "https://www.arduino.cc/" },
				{ img: "cs.png", linkInfo: "https://www.w3schools.com/cs/" },
				{ img: "python.png", linkInfo: "https://www.python.org/" },
				{ img: "centos.png", linkInfo: "https://www.centos.org/" },
				{
					img: "ps.png",
					linkInfo: "https://www.adobe.com/products/photoshop.html"
				},
				{ img: "xd.png", linkInfo: "https://www.adobe.com/products/xd.html" }
			],
			projects: [
				{
					title: "StreetTeca",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/StreetTeca",
						demo: "https://gustavo-vasconcelos.github.io/StreetTeca/"
					},
					description:
						"This project was developed during the 2nd semester of the 1st grade. The main purpose is to manage street libraries. There is no back-end involved, all information is kept locally (HTML Web Storage - Local Storage).",
					technologies: [
						"html",
						"css",
						"javascript",
						"bootstrap",
						"Google Maps API"
					],
					features: [
						"Manage users",
						"Manage libraries",
						"Manage edit gender & tags",
						"Manage authors",
						"Cathalog",
						"User profile",
						"Notifications",
						"Back-office"
					]
				},

				{
					title: "ATLAS",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/ATLAS",
						demo: "http://atlas-vue.herokuapp.com/"
					}
				},
				{
					title: "ATLAS API",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/ATLAS-server",
						demo: "https://documenter.getpostman.com/view/6874679/S1Zxbpdr"
					}
				},
				{
					title: "Pang 0.5",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/Pang-0.5",
						demo: "https://gustavo-vasconcelos.github.io/Pang-0.5/"
					}
				},
				{
					title: "Soccer Stars",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/Soccer-Stars"
					}
				},
				{
					title: "Felicia",
					url: {
						repository: "https://github.com/RodrigoQueiros/MAD-Game-Jam-2019"
					}
				}
			],
			modal: {
				active: false,
				project: {}
			},
			flickityOptions: {
				wrapAround: true,
			},
			form: {
				data: { email: "", subject: "", message: "" },
				sending: false,
				notification: false
			}
		}
	},
	created() {
		AOS.init()
	},
	mounted() {
		this.windowWidth = window.innerWidth
		window.addEventListener("resize", this.onResize)
	},
	methods: {
		onResize() {
			this.windowWidth = window.innerWidth
			if (this.windowWidth >= 600) {
				this.burgerActive = false
			}
		},
		burgerClicked() {
			this.burgerActive = !this.burgerActive
		},
		openModal(project) {
			if (project.description) {
				this.modal.project = project
				this.modal.active = true
			}
		},
		closeModal() {
			this.modal.active = false
		},
		clearForm() {
			this.form.data.email = ""
			this.form.data.subject = ""
			this.form.data.message = ""
		},
		async sendEmail() {
			this.form.sending = true

			await axios.post("https://api.emailjs.com/api/v1.0/email/send", {
				service_id: "gmail",
				template_id: "template_GvTYdBq4",
				user_id: "user_vdMPqb3V9ptqOOVsLKvSh",
				template_params: this.form.data
			})
			this.clearForm()
			this.form.sending = false
			this.form.notification = true
		}
	}
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Handlee|Raleway&display=swap");
@import url("../../node_modules/@fortawesome/fontawesome-free/css/all.min.css");

#header span {
	font-family: "Handlee", cursive;
}

#header .title {
	font-family: "Handlee", cursive;
	font-size: 2.5rem;
}

#header {
	//background-image: url("https://cdn.wallpapersafari.com/46/64/qc4PoO.jpg");
	background-image: url("../assets/img/bg.jpg");
	background-repeat: no-repeat;
	background-position: center;
}

section:not([is-one]) .container .title {
	font-family: "Raleway", sans-serif;
}

.navbar-menu.is-active {
	//background-color: white;
	text-align: left;
}

.navbar-menu.is-active a:hover {
	background-color: white;
	color: #406e8e;
	text-decoration: underline;
}

.navbar-item a {
	font-weight: bold;
	border-radius: 5px;
}

#about img {
	border-radius: 50%;
	box-shadow: 10px 10px 14px -4px rgba(0, 0, 0, 0.45);
	max-width: 200px;
}
.button-hover {
	color: #0b132b;
	transition: all 0.1s ease-out;
}
.button-hover:hover {
	color: white;
	transition: all 0.1s ease-in;
}
section hr {
	width: 100px;
	text-decoration: underline;
	margin: 0 auto 50px auto;
}

#skills img {
	width: 100px;
}

#skills img {
	width: 100px;
	transition: all 0.1s ease-in-out;
}
#skills img:hover {
	transform: scale(1.2);
	transition: all 0.1s ease-in-out;
}
.card {
	border-radius: 6px;
}
.card.column {
	padding: 0;
}
.card-content {
	cursor: pointer;
	padding: 0.5rem 0 0.5rem 0;
}
.card-image,
.card-footer-item span {
	cursor: pointer;
}

#projects .card:hover {
	transform: scale(1.02);
	transition: all 0.1s ease-in-out;
}

.modal-card-body {
	border-bottom-left-radius: 6px;
	border-bottom-right-radius: 6px;
}

.modal .content div + div {
	margin-top: 20px;
}
.modal .content div p,
.modal .content div ul {
	margin-top: 0;
	margin-bottom: 0;
}
#footer {
	padding: 1rem 0 1rem 0;
}
.notification {
	cursor: pointer;
}

.slide-fade-enter-active {
	transition: all 0.3s ease;
}
.slide-fade-leave-active {
	transition: all 0.3s ease;
}
.slide-fade-enter,
.slide-fade-leave-to {
	transform: translateX(10px);
	opacity: 0;
}
</style>
