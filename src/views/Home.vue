<template>
	<div>
		<nav class="navbar is-fixed-top has-background-one" role="navigation">
			<div class="navbar-brand">
				<a role="button" class="navbar-burger burger" :class="{ 'is-active': burgerActive }" @click="burgerClicked">
					<span aria-hidden="true"></span>
					<span aria-hidden="true"></span>
					<span aria-hidden="true"></span>
				</a>
			</div>

			<div class="navbar-menu" :class="{
				'is-active': burgerActive,
				'has-background-one': !burgerActive,
				'has-background-white': burgerActive,
			}" :style="!burgerActive
	? {
		marginLeft: (windowWidth * 8) / 1920 + 'rem',
		marginRight: (windowWidth * 8) / 1920 + 'rem',
	}
	: {}
	" @click="burgerClicked && windowWidth < 600">
				<div class="navbar-start">
					<div class="navbar-item">
						<a class="navbar-item" :class="!burgerActive ? 'has-text-white' : ''" v-scroll-to="'#about'"
							@click="burgerActive = false">About me</a>
						<a class="navbar-item" :class="!burgerActive ? 'has-text-white' : ''" v-scroll-to="'#skills'"
							@click="burgerActive = false">Skills</a>
						<a class="navbar-item" :class="!burgerActive ? 'has-text-white' : ''" v-scroll-to="'#projects'"
							@click="burgerActive = false">Projects</a>
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
						<span> <strike>world</strike> </span>! I'm
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
						<img class="is-rounded" src="../assets/img/me.jpeg" />
						<div class="columns is-centered" style="margin-top: 5px">
							<a href="https://github.com/gustavo-vasconcelos/" class="has-text-two" target="_blank">
								<span class="icon is-large" style="font-size: 22px"><i class="fab fa-github"
										aria-hidden="true"></i></span>
							</a>
							<a href="https://www.linkedin.com/in/gustavo-vasconcelos/" class="has-text-two" target="_blank">
								<span class="icon is-large" style="font-size: 22px"><i class="fab fa-linkedin"
										aria-hidden="true"></i></span>
							</a>
						</div>
					</div>
					<div class="column is-centered has-text-justified has-text-white" data-aos="fade-left">
						<p>
							I'm a developer with experience in web development, IoT solutions and API integration.
							I also find the web development and IT field very fascinating and interesting, because we use
							applications and services developed with these technologies in our daily lives.
							During my academic studies at <a href="http://esmad.ipp.pt" target="_blank"
								class="has-text-four">ESMAD (P.PORTO)</a>, I have developed many projects of which I'm very
							proud of.
							I'm proficient in both front and back end areas, but I like back-end the most.
						</p>
						<br />
						<p>
							I find the web development and IT field very fascinating and
							interesting, because we use applications and services developed
							with these technologies in our daily lives.
						</p>
						<br />
						<p>
							During this last years, I've been developing many projects of
							which I'm very proud, under my academic studies and professional
							duties.
						</p>
					</div>
				</div>
			</div>
		</section>
		<section id="skills" class="section has-background-white">
			<div class="container">
				<h1 class="title has-text-black">Skills</h1>
				<hr class="has-background-black" />
				<div class="tabs is-toggle is-toggle-rounded is-fullwidth">
					<ul>
						<li :class="selectedSkills.all ? 'is-active' : ''" @click="changedSelectedSkills('all')">
							<a>
								<span class="icon is-small"><i class="fas fa-th" aria-hidden="true"></i></span>
								<span>All</span>
							</a>
						</li>
						<li :class="selectedSkills.languages ? 'is-active' : ''"
							@click="changedSelectedSkills('languages')">
							<a>
								<span class="icon is-small"><i class="fas fa-code" aria-hidden="true"></i></span>
								<span>Languages</span>
							</a>
						</li>
						<li :class="selectedSkills.technologies ? 'is-active' : ''"
							@click="changedSelectedSkills('technologies')">
							<a>
								<span class="icon is-small"><i class="fas fa-cogs" aria-hidden="true"></i></span>
								<span>Technologies</span>
							</a>
						</li>
						<li :class="selectedSkills.softwares ? 'is-active' : ''"
							@click="changedSelectedSkills('softwares')">
							<a>
								<span class="icon is-small"><i class="far fa-window-restore" aria-hidden="true"></i></span>
								<span>Softwares</span>
							</a>
						</li>
					</ul>
				</div>
				<br />
				<div class="columns is-mobile is-multiline">
					<template v-for="(skill, index) in skills">
						<div v-if="selectedSkills.all ||
							selectedSkills[skill.type] ||
							selectedSkills[skill.type] === 'all'
							" class="column is-2-widescreen is-3-tablet is-4-mobile" :key="'skill_' + index" data-aos="fade-in">
							<a :href="skill.linkInfo" target="_blank">
								<img :title="skill.title" :src="require(`@/assets/img/skills/${skill.img}`)" />
							</a>
						</div>
					</template>
				</div>
			</div>
		</section>
		<section id="projects" class="section has-background-three">
			<div class="container">
				<h1 class="title has-text-white">Projects</h1>
				<hr />
				<div class="columns is-multiline">
					<div class="column is-4-widescreen is-6-tablet" v-for="(project, index) in projects"
						:key="'project_' + index" data-aos="fade-in">
						<div class="card">
							<div class="card-content" @click="openModal(project)">
								<p class="is-size-4">{{ project.title }}</p>
							</div>
							<div class="card-image" @click="openModal(project)">
								<figure class="image">
									<img :src="require(`@/assets/img/projects/${project.title
										.toLowerCase()
										.replace(/ /g, '')}/thumb.jpg`)
										" alt />
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
		<div class="modal" :class="{ 'is-active': modal.active }" v-if="modal.active">
			<div class="modal-background" @click="closeModal" data-aos="fade-in"></div>
			<div class="modal-card" data-aos="fade-up">
				<header class="modal-card-head">
					<p class="modal-card-title">{{ modal.project.title }}</p>
					<button class="delete" aria-label="close" @click="closeModal"></button>
				</header>
				<section class="modal-card-body has-text-left">
					<img v-if="modal.active && !modal.project.url.promotionalVideo" :src="require(`../assets/img/projects/${modal.project.title
						.toLowerCase()
						.replace(/ /g, '')}/thumb.jpg`)
						" />
					<iframe v-else-if="modal.project.url.promotionalVideo" width="100%" height="350"
						:src="`https://www.youtube.com/embed/${modal.project.url.promotionalVideo}`" frameborder="0"
						allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
						allowfullscreen></iframe>
					<div class="content">
						<div>
							<p class="is-size-5">Description</p>
							<div v-html="modal.project.description"></div>
						</div>
						<div>
							<p class="is-size-5">Technologies</p>
							<ul>
								<li v-for="(technology, index) in modal.project.technologies" :key="'technology_' + index">
									{{ technology }}
								</li>
							</ul>
						</div>
						<div v-if="modal.project.features">
							<p class="is-size-5">Main features</p>
							<ul>
								<template v-for="(feature, index) in modal.project.features">
									<li v-if="feature[0].length === 1" :key="'feature_' + index">
										{{ feature }}
									</li>
									<li :key="'feature_' + index + 2" v-else>
										{{ feature[0] }}
										<ul>
											<template v-for="(subfeature, subIndex) in feature">
												<li v-if="subIndex > 0" :key="'subfeature_' + subIndex">
													{{ subfeature }}
												</li>
											</template>
										</ul>
									</li>
								</template>
							</ul>
						</div>
						<div v-if="modal.project.screenshots > 0">
							<p class="is-size-5">Screenshots:</p>
							<carousel :per-page="1" :centerMode="true" style="margin: 0">
								<slide data-index="0" data-name="MySlideName"
									v-for="(screenshot, index) in modal.project.screenshots" :key="'screnshot_' + index"
									style="margin: 0">
									<img :src="require(`../assets/img/projects/${modal.project.title
										.toLowerCase()
										.replace(/ /g, '')}/screenshots/${index}.jpg`)
										" />
								</slide>
							</carousel>
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
						<div class="notification is-two" v-if="form.notification" @click="form.notification = false"
							data-aos="fade">
							Your message was sent. I'll reply you ASAP.
						</div>
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
									<textarea id="message" class="textarea" name="message" v-model="form.data.message"
										required></textarea>
								</div>
							</div>
							<button type="submit" class="button is-two is-fullwidth"
								:class="{ 'is-loading': form.sending }">
								Send
							</button>
						</form>
					</div>
				</div>
			</div>
		</section>
		<footer id="footer" class="has-background-two has-text-white is-centered">
			<p style="margin-top: 10px">
				Copyright &copy; 2019-2023 Gustavo Vasconcelos
			</p>
		</footer>
	</div>
</template>

<script>
import AOS from "aos"
import axios from "axios"

export default {
	name: "home",
	data() {
		return {
			windowWidth: 0,
			burgerActive: false,
			selectedSkills: {
				all: true,
				languages: false,
				technologies: false,
				softwares: false,
			},
			skills: [
				{
					title: "HTML",
					type: "languages",
					img: "html.png",
					linkInfo: "https://developer.mozilla.org/en-US/docs/Glossary/HTML",
				},
				{
					title: "CSS",
					type: "languages",
					img: "css.png",
					linkInfo: "https://developer.mozilla.org/en-US/docs/Glossary/CSS",
				},
				{
					title: "JavaScript",
					type: "languages",
					img: "js.png",
					linkInfo: "https://developer.mozilla.org/en-US/docs/Web/JavaScript",
				},
				{
					title: "Visual Studio Code",
					type: "softwares",
					img: "vscode.png",
					linkInfo: "https://code.visualstudio.com/",
				},
				{
					title: "Bootstrap",
					type: "technologies",
					img: "bootstrap.png",
					linkInfo: "https://getbootstrap.com/",
				},
				{
					title: "Bulma",
					type: "technologies",
					img: "bulma.png",
					linkInfo: "https://bulma.io/",
				},
				{
					title: "Vue.js",
					type: "technologies",
					img: "vue.png",
					linkInfo: "https://vuejs.org/",
				},
				{
					title: "npm",
					type: "technologies",
					img: "npm.png",
					linkInfo: "https://www.npmjs.com/",
				},
				{
					title: "Node.js",
					type: "technologies",
					img: "node.png",
					linkInfo: "https://nodejs.org/",
				},
				{
					type: "technologies",
					img: "express.png",
					linkInfo: "https://expressjs.com/",
				},
				{
					title: "Express",
					type: "technologies",
					img: "twx.png",
					linkInfo: "https://www.ptc.com/en/products/iiot/thingworx-platform/",
				},
				{
					title: "Vuforia",
					type: "technologies",
					img: "vuforia.png",
					linkInfo: "https://www.ptc.com/en/products/vuforia/",
				},
				{
					title: "MongoDB",
					type: "technologies",
					img: "mongo.png",
					linkInfo: "https://www.mongodb.com/",
				},
				{
					title: "Robo3T",
					type: "softwares",
					img: "robo3t.png",
					linkInfo: "https://www.mongodb.com/",
				},
				{
					title: "Docker",
					type: "technologies",
					img: "docker.png",
					linkInfo: "https://www.docker.com/",
				},
				{
					title: "MySQL",
					type: "softwares",
					img: "mysql.png",
					linkInfo: "https://www.mysql.com/",
				},
				{
					title: "Git",
					type: "technologies",
					img: "git.png",
					linkInfo: "https://git-scm.com/",
				},
				{
					title: "Socket.io",
					type: "technologies",
					img: "socketio.png",
					linkInfo: "https://socket.io/",
				},
				{
					title: "Postman",
					type: "softwares",
					img: "postman.png",
					linkInfo: "https://www.postman.com/",
				},
				{
					title: "Three.js",
					type: "technologies",
					img: "three.png",
					linkInfo: "https://threejs.org/",
				},
				{
					title: "Arduino",
					type: "softwares",
					img: "arduino.png",
					linkInfo: "https://www.arduino.cc/",
				},
				{
					title: "Java",
					type: "languages",
					img: "java.png",
					linkInfo: "https://java.com/",
				},
				{
					title: "Python",
					type: "languages",
					img: "python.png",
					linkInfo: "https://www.python.org/",
				},
				{
					title: "C#",
					type: "languages",
					img: "cs.png",
					linkInfo: "https://www.w3schools.com/cs/",
				},
				{
					title: "CentOS",
					type: "all",
					img: "centos.png",
					linkInfo: "https://www.centos.org/",
				},
				{
					title: "Bash",
					type: "languages",
					img: "bash.png",
					linkInfo: "https://www.centos.org/",
				},
				{
					title: "Adobe Photoshop",
					type: "softwares",
					img: "ps.png",
					linkInfo: "https://www.adobe.com/products/photoshop.html",
				},
				{
					title: "Adobe Xd",
					type: "softwares",
					img: "xd.png",
					linkInfo: "https://www.adobe.com/products/xd.html",
				},
				{
					title: "Jira",
					type: "softwares",
					img: "jira.png",
					linkInfo: "https://www.atlassian.com/software/jira",
				},
			],
			projects: [
				{
					title: "Dynamic Report Generator",
					url: {
						promotionalVideo: "z9MUiflG63I",
					},
					description:
						"This project was developed by within the scope of my curricular internship - Bachelor’s Degree in Web Information Systems and Technologies, at ESMAD.<br>It was a web application for internal use developed at Celfocus, a subsidiary of Novabase, one of the leaders in the telecommunications sector.<br>More and more companies are looking for new ways to automate processes, so that every resource is maximized. This project is basically an automation, so the whole process of planning, development and implementation is here described. This application has as main objective the generation of automated reports through processes and information executed in external tools, by Quality Assurance engineers. These reports are used for the purpose of internal and external documentation.<br><br>If you wish to see this project report please contact me below.",
					technologies: [
						"html",
						"css",
						"javascript",
						"vue.js",
						"vuetify",
						"axios",
						"simpleMDE",
						"express",
						"mongo",
						"mongoose",
						"REST",
						"jwt",
						"docker",
						"socket.io",
					],
					features: [
						"Generate test case specification report from TestRail and TM4J",
						"Generate test execution report from TestRail and TM4J",
						"Generate SIT report from a Jira project",
						"Export test cases from TestRail to TM4J",
						"See report history",
						"See live progress generation info",
						"Edit report after generation",
					],
					screenshots: 3,
				},
				{
					title: "Security System",
					url: {
						demo: "https://www.youtube.com/watch?v=Q1tRANREx",
						promotionalVideo: "Q1tRANREx-c",
					},
					description:
						"This project was developed as final project to the Computational Systems course unit, in order to practise all knowledge learnt. It was managed to create a password protected 'vault' that was locked/unlocked using a servo motor.",
					technologies: ["arduino"],
					features: [
						"Lock/unlock the door",
						"LCD displaying all info",
						"Password protection inserted by remote control",
					],
					screenshots: 0,
				},
				{
					title: "StreetTeca",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/StreetTeca",
						demo: "https://gustavo-vasconcelos.github.io/StreetTeca/",
					},
					description:
						"This project was developed during the 2nd semester of the 1st grade. The main purpose is to manage street libraries. There is no back-end involved, all information is kept locally (HTML Web Storage - Local Storage).",
					technologies: [
						"html",
						"css",
						"javascript",
						"bootstrap",
						"Google Maps API",
					],
					features: [
						"Manage users",
						"Manage libraries",
						"Manage edit gender & tags",
						"Manage authors",
						"Cathalog",
						"User profile",
						"Notifications",
						"Back-office",
					],
					screenshots: 4,
				},
				{
					title: "ATLAS",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/ATLAS",
						promotionalVideo: "pC-v98n7apU",
					},
					description:
						"This project is a web application developed during the 2nd year in the Web Information Systems and Technologies course for the Web Programming I subject at ESMAD. The main objective was to develop an app that allowed users to enroll in school events which were created by teachers or admins.",
					technologies: [
						"html",
						"css",
						"scss",
						"bootstrap",
						"javascript",
						"vue.js",
						"axios",
					],
					features: [
						"Three different authetication profiles (student, event proponent, admin).",
						"Workshops/events Publishing and Enrollment.",
						"Idea discussion forum, open to students and event proponents.",
						"Gamification elements to improve the User Experience.",
					],
					screenshots: 0,
				},
				{
					title: "ATLAS API",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/ATLAS-server",
						demo: "https://documenter.getpostman.com/view/6874679/S1Zxbpdr",
					},
					description:
						"This REST API was developed to feed all the data to the ATLAS web application. It was developed accordingly the MVC pattern. It's fully documented and functional.",
					technologies: [
						"javascript",
						"node.js",
						"express",
						"mongo",
						"mongoose",
						"REST",
						"jwt",
						"cookies",
					],
					screenshots: 0,
				},
				{
					title: "Pang 0.5",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/Pang-0.5",
						demo: "https://gustavo-vasconcelos.github.io/Pang-0.5/",
					},
					description:
						"Developing this game was a final project of a curricular unit. It was coded in plain JavaScript with HTML5 Canvas.",
					technologies: ["javascript", "html5 canvas"],
					screenshots: 2,
				},
				{
					title: "Soccer Stars",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/Soccer-Stars",
					},
					description:
						"This game was developed as a project of Physics for Programming where the goal was to make a game in Python using all physic theories learnt.",
					technologies: ["python", "pygame"],
					screenshots: 0,
				},
				{
					title: "Felicia",
					url: {
						repository: "https://github.com/gustavo-vasconcelos/Felicia",
						demo: "https://gustavo-vasconcelos.github.io/Felicia/",
					},
					description:
						"This game was developed during MAD Game Jam 2019. We had 48 hours to develop a game, and the final outcome was Felicia.",
					technologies: ["javascript", "html5 canvas"],
					screenshots: 0,
				},
			],
			modal: {
				active: false,
				project: {},
			},
			flickityOptions: {
				wrapAround: true,
			},
			form: {
				data: { email: "", subject: "", message: "" },
				sending: false,
				notification: false,
			},
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
		changedSelectedSkills(skill) {
			this.selectedSkills.all = false
			this.selectedSkills.languages = false
			this.selectedSkills.technologies = false
			this.selectedSkills.softwares = false

			this.selectedSkills[skill] = true
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
				template_params: this.form.data,
			})
			this.clearForm()
			this.form.sending = false
			this.form.notification = true
		},
	},
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Solway|Share+Tech+Mono&display=swap");
@import url("../../node_modules/@fortawesome/fontawesome-free/css/all.min.css");

#header span {
	font-family: "Share+Tech+Mono", monospace;
}

#header .title {
	font-family: "Share+Tech+Mono", monospace;
	font-size: 2rem;
	font-weight: 600;
}

#header {
	background-image: url("../assets/img/bg.jpg");
	background-repeat: no-repeat;
	background-position: center;
}

section:not([is-one]) .container .title {
	font-family: "Solway", serif;
	font-weight: 600;
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
	color: #406e8e;
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

#projects .card .card-content p {
	font-family: "Solway", serif;
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

.modal .content div+div {
	margin-top: 20px;
}

.VueCarousel-pagination,
.VueCarousel-dot-container {
	margin-top: 0 !important;
}

.modal .content div p,
.modal .content div ul {
	margin-top: 0;
	margin-bottom: 0;
}

#footer {
	padding: 1.5rem 0 1.5rem 0;
	font-size: 11px;
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

#contact button {
	font-family: "Montserrat", sans-serif;
}

#skills .is-active a {
	background-color: #1C2541;
	border: 1px solid #1C2541;
}
</style>
