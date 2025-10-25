<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Vue Portfolio</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-color: #2c3e50;
            --secondary-color: #42b883;
            --accent-color: #ff6b6b;
            --text-color: #2c3e50;
            --bg-color: #ffffff;
            --gray-light: #f8f9fa;
            --dark-bg: #1a1a1a;
            --dark-text: #ffffff;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: var(--text-color);
            transition: background-color 0.3s, color 0.3s;
        }

        body.dark-mode {
            background-color: var(--dark-bg);
            color: var(--dark-text);
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 2rem;
        }

        /* Navigation */
        .navbar {
            position: fixed;
            top: 0;
            width: 100%;
            padding: 1rem 0;
            background: transparent;
            transition: all 0.3s ease;
            z-index: 1000;
        }

        .navbar.scrolled {
            background: var(--bg-color);
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            padding: 0.5rem 0;
        }

        .dark-mode .navbar.scrolled {
            background: var(--dark-bg);
            box-shadow: 0 2px 10px rgba(255,255,255,0.1);
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .nav-logo a {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary-color);
            text-decoration: none;
        }

        .dark-mode .nav-logo a {
            color: var(--dark-text);
        }

        .nav-menu {
            display: flex;
            gap: 2rem;
        }

        .nav-link {
            color: var(--text-color);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s ease;
            position: relative;
            cursor: pointer;
        }

        .dark-mode .nav-link {
            color: var(--dark-text);
        }

        .nav-link:hover,
        .nav-link.active {
            color: var(--secondary-color);
        }

        .nav-link.active::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 2px;
            background: var(--secondary-color);
        }

        .theme-toggle {
            background: none;
            border: none;
            font-size: 1.2rem;
            cursor: pointer;
            color: var(--text-color);
            transition: color 0.3s ease;
        }

        .dark-mode .theme-toggle {
            color: var(--dark-text);
        }

        .hamburger {
            display: none;
            flex-direction: column;
            cursor: pointer;
        }

        .hamburger span {
            width: 25px;
            height: 3px;
            background: var(--primary-color);
            margin: 3px 0;
            transition: 0.3s;
        }

        .dark-mode .hamburger span {
            background: var(--dark-text);
        }

        /* Hero Section */
        .home {
            padding-top: 80px;
        }

        .hero {
            max-width: 1200px;
            margin: 0 auto;
            padding: 4rem 2rem;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
            min-height: 100vh;
        }

        .hero-title {
            font-size: 3rem;
            margin-bottom: 1rem;
            color: var(--primary-color);
        }

        .dark-mode .hero-title {
            color: var(--dark-text);
        }

        .highlight {
            color: var(--secondary-color);
        }

        .hero-subtitle {
            font-size: 1.5rem;
            color: var(--secondary-color);
            margin-bottom: 1rem;
        }

        .hero-description {
            font-size: 1.1rem;
            margin-bottom: 2rem;
            color: #666;
            line-height: 1.6;
        }

        .dark-mode .hero-description {
            color: #ccc;
        }

        .hero-buttons {
            display: flex;
            gap: 1rem;
        }

        .btn {
            padding: 0.75rem 2rem;
            border: none;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
        }

        .btn-primary {
            background: var(--secondary-color);
            color: white;
        }

        .btn-primary:hover {
            background: #369c6f;
            transform: translateY(-2px);
        }

        .btn-secondary {
            background: transparent;
            color: var(--primary-color);
            border: 2px solid var(--primary-color);
        }

        .dark-mode .btn-secondary {
            color: var(--dark-text);
            border-color: var(--dark-text);
        }

        .btn-secondary:hover {
            background: var(--primary-color);
            color: white;
            transform: translateY(-2px);
        }

        .dark-mode .btn-secondary:hover {
            background: var(--dark-text);
            color: var(--dark-bg);
        }

        .hero-image {
            display: flex;
            justify-content: center;
        }

        .image-placeholder {
            width: 300px;
            height: 300px;
            background: var(--gray-light);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 5px solid var(--secondary-color);
            color: #666;
            font-weight: bold;
        }

        .dark-mode .image-placeholder {
            background: #333;
            color: #ccc;
        }

        /* Skills Section */
        .skills-section {
            background: var(--gray-light);
            padding: 4rem 0;
        }

        .dark-mode .skills-section {
            background: #2d2d2d;
        }

        .skills-section h2 {
            text-align: center;
            margin-bottom: 3rem;
            font-size: 2.5rem;
            color: var(--primary-color);
        }

        .dark-mode .skills-section h2 {
            color: var(--dark-text);
        }

        .skills-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
        }

        .skill-card {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .dark-mode .skill-card {
            background: #3d3d3d;
            box-shadow: 0 5px 15px rgba(255,255,255,0.1);
        }

        .skill-card:hover {
            transform: translateY(-5px);
        }

        .skill-icon {
            font-size: 3rem;
            color: var(--secondary-color);
            margin-bottom: 1rem;
        }

        .skill-card h3 {
            margin-bottom: 1rem;
            color: var(--primary-color);
        }

        .dark-mode .skill-card h3 {
            color: var(--dark-text);
        }

        /* Portfolio Section */
        .portfolio {
            padding: 100px 0 50px;
            min-height: 100vh;
        }

        .page-title {
            text-align: center;
            font-size: 3rem;
            margin-bottom: 1rem;
            color: var(--primary-color);
        }

        .dark-mode .page-title {
            color: var(--dark-text);
        }

        .page-subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 3rem;
            font-size: 1.2rem;
        }

        .dark-mode .page-subtitle {
            color: #ccc;
        }

        .filter-buttons {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 3rem;
            flex-wrap: wrap;
        }

        .filter-btn {
            padding: 0.5rem 1.5rem;
            border: 2px solid var(--secondary-color);
            background: transparent;
            color: var(--secondary-color);
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .filter-btn.active,
        .filter-btn:hover {
            background: var(--secondary-color);
            color: white;
        }

        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 2rem;
        }

        .project-card {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .dark-mode .project-card {
            background: #3d3d3d;
            box-shadow: 0 5px 15px rgba(255,255,255,0.1);
        }

        .project-card:hover {
            transform: translateY(-5px);
        }

        .project-image {
            position: relative;
            height: 250px;
            overflow: hidden;
            background: var(--gray-light);
            display: flex;
            align-items: center;
            justify-content: center;
            color: #666;
            font-weight: bold;
        }

        .dark-mode .project-image {
            background: #2d2d2d;
            color: #ccc;
        }

        .project-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .project-card:hover .project-overlay {
            opacity: 1;
        }

        .project-links {
            display: flex;
            gap: 1rem;
        }

        .project-link {
            width: 50px;
            height: 50px;
            background: var(--secondary-color);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            text-decoration: none;
            transition: background 0.3s ease;
        }

        .project-link:hover {
            background: var(--primary-color);
        }

        .project-info {
            padding: 1.5rem;
        }

        .project-info h3 {
            margin-bottom: 0.5rem;
            color: var(--primary-color);
        }

        .dark-mode .project-info h3 {
            color: var(--dark-text);
        }

        .project-info p {
            color: #666;
            margin-bottom: 1rem;
            line-height: 1.5;
        }

        .dark-mode .project-info p {
            color: #ccc;
        }

        .project-tech {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
        }

        .tech-tag {
            background: var(--gray-light);
            color: var(--primary-color);
            padding: 0.25rem 0.75rem;
            border-radius: 15px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        .dark-mode .tech-tag {
            background: #4d4d4d;
            color: var(--dark-text);
        }

        /* About Section */
        .about {
            padding: 100px 0 50px;
            min-height: 100vh;
        }

        .about-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
        }

        .about-text h2 {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
            color: var(--primary-color);
        }

        .dark-mode .about-text h2 {
            color: var(--dark-text);
        }

        .about-text p {
            margin-bottom: 1.5rem;
            line-height: 1.8;
            color: #666;
        }

        .dark-mode .about-text p {
            color: #ccc;
        }

        /* Contact Section */
        .contact {
            padding: 100px 0 50px;
            min-height: 100vh;
        }

        .contact-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
        }

        .contact-info {
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }

        .contact-item {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .contact-icon {
            width: 50px;
            height: 50px;
            background: var(--secondary-color);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.2rem;
        }

        .contact-form {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .dark-mode .contact-form {
            background: #3d3d3d;
            box-shadow: 0 5px 15px rgba(255,255,255,0.1);
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: var(--primary-color);
        }

        .dark-mode .form-group label {
            color: var(--dark-text);
        }

        .form-control {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
            background: var(--bg-color);
            color: var(--text-color);
        }

        .dark-mode .form-control {
            background: #4d4d4d;
            border-color: #666;
            color: var(--dark-text);
        }

        .form-control:focus {
            outline: none;
            border-color: var(--secondary-color);
        }

        textarea.form-control {
            resize: vertical;
            min-height: 120px;
        }

        /* Footer */
        .footer {
            background: var(--primary-color);
            color: white;
            text-align: center;
            padding: 2rem 0;
            margin-top: 4rem;
        }

        .dark-mode .footer {
            background: #2d2d2d;
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 1rem;
        }

        .social-link {
            width: 40px;
            height: 40px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            text-decoration: none;
            transition: background 0.3s ease;
        }

        .social-link:hover {
            background: var(--secondary-color);
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .hamburger {
                display: flex;
            }

            .nav-menu {
                position: fixed;
                top: 70px;
                left: -100%;
                width: 100%;
                height: calc(100vh - 70px);
                background: var(--bg-color);
                flex-direction: column;
                justify-content: flex-start;
                align-items: center;
                padding-top: 2rem;
                transition: left 0.3s ease;
            }

            .dark-mode .nav-menu {
                background: var(--dark-bg);
            }

            .nav-menu.active {
                left: 0;
            }

            .nav-link {
                padding: 1rem 0;
                font-size: 1.2rem;
            }

            .hero {
                grid-template-columns: 1fr;
                text-align: center;
                gap: 2rem;
            }

            .hero-title {
                font-size: 2rem;
            }

            .hero-buttons {
                justify-content: center;
                flex-wrap: wrap;
            }

            .image-placeholder {
                width: 200px;
                height: 200px;
            }

            .projects-grid {
                grid-template-columns: 1fr;
            }

            .filter-buttons {
                gap: 0.5rem;
            }

            .filter-btn {
                padding: 0.5rem 1rem;
                font-size: 0.9rem;
            }

            .about-content,
            .contact-grid {
                grid-template-columns: 1fr;
                gap: 2rem;
            }
        }
    </style>
</head>
<body>
    <div id="app">
        <!-- Navigation -->
        <nav class="navbar" :class="{ 'scrolled': isScrolled }">
            <div class="nav-container">
                <div class="nav-logo">
                    <a href="#" @click="changePage('home')">Portfolio</a>
                </div>
                <div class="nav-menu" :class="{ 'active': isMenuOpen }">
                    <a 
                        v-for="item in navItems" 
                        :key="item.name"
                        :class="['nav-link', { 'active': currentPage === item.id }]"
                        @click="changePage(item.id)"
                    >
                        {{ item.name }}
                    </a>
                    <button class="theme-toggle" @click="toggleDarkMode">
                        <i :class="darkMode ? 'fas fa-sun' : 'fas fa-moon'"></i>
                    </button>
                </div>
                <div class="hamburger" @click="toggleMenu">
                    <span></span>
                    <span></span>
                    <span></span>
                </div>
            </div>
        </nav>

        <!-- Home Page -->
        <div v-if="currentPage === 'home'" class="home">
            <section class="hero">
                <div class="hero-content">
                    <h1 class="hero-title">Hi, I'm <span class="highlight">{{ name }}</span></h1>
                    <p class="hero-subtitle">{{ title }}</p>
                    <p class="hero-description">
                        {{ description }}
                    </p>
                    <div class="hero-buttons">
                        <button class="btn btn-primary" @click="changePage('portfolio')">
                            View My Work
                        </button>
                        <button class="btn btn-secondary" @click="changePage('contact')">
                            Contact Me
                        </button>
                    </div>
                </div>
                <div class="hero-image">
                    <div class="image-placeholder">
                        Your Photo
                    </div>
                </div>
            </section>

            <section class="skills-section">
                <div class="container">
                    <h2>Technologies I Use</h2>
                    <div class="skills-grid">
                        <div v-for="skill in skills" :key="skill.name" class="skill-card">
                            <div class="skill-icon">
                                <i :class="skill.icon"></i>
                            </div>
                            <h3>{{ skill.name }}</h3>
                            <p>{{ skill.description }}</p>
                        </div>
                    </div>
                </div>
            </section>
        </div>

        <!-- Portfolio Page -->
        <div v-if="currentPage === 'portfolio'" class="portfolio">
            <div class="container">
                <h1 class="page-title">My Portfolio</h1>
                <p class="page-subtitle">Some of my recent projects</p>

                <div class="filter-buttons">
                    <button 
                        v-for="filter in filters" 
                        :key="filter"
                        :class="['filter-btn', { active: activeFilter === filter }]"
                        @click="activeFilter = filter"
                    >
                        {{ filter }}
                    </button>
                </div>

                <div class="projects-grid">
                    <div 
                        v-for="project in filteredProjects" 
                        :key="project.id"
                        class="project-card"
                    >
                        <div class="project-image">
                            Project Image
                            <div class="project-overlay">
                                <div class="project-links">
                                    <a :href="project.demo" target="_blank" class="project-link">
                                        <i class="fas fa-external-link-alt"></i>
                                    </a>
                                    <a :href="project.github" target="_blank" class="project-link">
                                        <i class="fab fa-github"></i>
                                    </a>
                                </div>
                            </div>
                        </div>
                        <div class="project-info">
                            <h3>{{ project.title }}</h3>
                            <p>{{ project.description }}</p>
                            <div class="project-tech">
                                <span 
                                    v-for="tech in project.technologies" 
                                    :key="tech"
                                    class="tech-tag"
                                >
                                    {{ tech }}
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- About Page -->
        <div v-if="currentPage === 'about'" class="about">
            <div class="container">
                <h1 class="page-title">About Me</h1>
                <div class="about-content">
                    <div class="about-text">
                        <h2>Hello! I'm {{ name }}</h2>
                        <p>
                            I'm a passionate {{ title.toLowerCase() }} with experience in creating 
                            modern web applications. I love turning complex problems into simple, 
                            beautiful designs.
                        </p>
                        <p>
                            My journey in web development started {{ experience }} years ago, and 
                            I've been constantly learning and adapting to new technologies ever since.
                        </p>
                        <p>
                            When I'm not coding, you can find me exploring new technologies, 
                            contributing to open-source projects, or enjoying outdoor activities.
                        </p>
                        <div class="hero-buttons">
                            <button class="btn btn-primary" @click="changePage('contact')">
                                Get In Touch
                            </button>
                            <a :href="resumeLink" class="btn btn-secondary" target="_blank">
                                Download CV
                            </a>
                        </div>
                    </div>
                    <div class="about-image">
                        <div class="image-placeholder" style="width: 400px; height: 400px;">
                            About Me Photo
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Contact Page -->
        <div v-if="currentPage === 'contact'" class="contact">
            <div class="container">
                <h1 class="page-title">Get In Touch</h1>
                <p class="page-subtitle">Let's work together!</p>

                <div class="contact-grid">
                    <div class="contact-info">
                        <div class="contact-item">
                            <div class="contact-icon">
                                <i class="fas fa-envelope"></i>
                            </div>
                            <div>
                                <h3>Email</h3>
                                <p>{{ email }}</p>
                            </div>
                        </div>
                        <div class="contact-item">
                            <div class="contact-icon">
                                <i class="fas fa-phone"></i>
                            </div>
                            <div>
                                <h3>Phone</h3>
                                <p>{{ phone }}</p>
                            </div>
                        </div>
                        <div class="contact-item">
                            <div class="contact-icon">
                                <i class="fas fa-map-marker-alt"></i>
                            </div>
                            <div>
                                <h3>Location</h3>
                                <p>{{ location }}</p>
                            </div>
                        </div>
                    </div>

                    <div class="contact-form">
                        <form @submit.prevent="submitForm">
                            <div class="form-group">
                                <label for="name">Name</label>
                                <input type="text" id="name" class="form-control" v-model="form.name" required>
                            </div>
                            <div class="form-group">
                                <label for="email">Email</label>
                                <input type="email" id="email" class="form-control" v-model="form.email" required>
                            </div>
                            <div class="form-group">
                                <label for="subject">Subject</label>
                                <input type="text" id="subject" class="form-control" v-model="form.subject" required>
                            </div>
                            <div class="form-group">
                                <label for="message">Message</label>
                                <textarea id="message" class="form-control" v-model="form.message" required></textarea>
                            </div>
                            <button type="submit" class="btn btn-primary" style="width: 100%;">
                                Send Message
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </div>

        <!-- Footer -->
        <footer class="footer">
            <div class="container">
                <div class="social-links">
                    <a v-for="social in socialLinks" :key="social.name" :href="social.url" class="social-link" target="_blank">
                        <i :class="social.icon"></i>
                    </a>
                </div>
                <p>&copy; 2024 {{ name }}. All rights reserved.</p>
            </div>
        </footer>
    </div>

    <script>
        new Vue({
            el: '#app',
            data: {
                currentPage: 'home',
                isScrolled: false,
                isMenuOpen: false,
                darkMode: false,
                activeFilter: 'All',
                
                // Personal Information
                name: 'John Doe',
                title: 'Frontend Developer',
                description: 'I create beautiful and functional web applications with modern technologies like Vue.js, React, and Node.js.',
                experience: 3,
                email: 'john.doe@email.com',
                phone: '+1 (555) 123-4567',
                location: 'New York, NY',
                resumeLink: '#',
                
                // Navigation
                navItems: [
                    { name: 'Home', id: 'home' },
                    { name: 'Portfolio', id: 'portfolio' },
                    { name: 'About', id: 'about' },
                    { name: 'Contact', id: 'contact' }
                ],
                
                // Skills
                skills: [
                    {
                        name: 'Vue.js',
                        icon: 'fab fa-vuejs',
                        description: 'Modern JavaScript framework for building user interfaces'
                    },
                    {
                        name: 'JavaScript',
                        icon: 'fab fa-js-square',
                        description: 'Programming language for interactive web experiences'
                    },
                    {
                        name: 'CSS3',
                        icon: 'fab fa-css3-alt',
                        description: 'Styling and layout for beautiful web designs'
                    },
                    {
                        name: 'Git',
                        icon: 'fab fa-git-alt',
                        description: 'Version control for collaborative development'
                    }
                ],
                
                // Portfolio
                filters: ['All', 'Vue.js', 'JavaScript', 'CSS', 'React'],
                projects: [
                    {
                        id: 1,
                        title: 'E-Commerce Website',
                        description: 'A full-featured online store built with Vue.js and Vuex with shopping cart and payment integration.',
                        image: '/images/project1.jpg',
                        demo: 'https://demo.com',
                        github: 'https://github.com/username/project1',
                        technologies: ['Vue.js', 'Vuex', 'CSS3', 'Firebase'],
                        category: 'Vue.js'
                    },
                    {
                        id: 2,
                        title: 'Task Management App',
                        description: 'Productivity app for managing daily tasks and projects with drag-and-drop functionality.',
                        image: '/images/project2.jpg',
                        demo: 'https://demo.com',
                        github: 'https://github.com/username/project2',
                        technologies: ['JavaScript', 'HTML5', 'CSS3', 'LocalStorage'],
                        category: 'JavaScript'
                    },
                    {
                        id: 3,
                        title: 'Weather Dashboard',
                        description: 'Real-time weather application with forecast and location-based services.',
                        image: '/images/project3.jpg',
                        demo: 'https://demo.com',
                        github: 'https://github.com/username/project3',
                        technologies: ['React', 'API', 'CSS3', 'Chart.js'],
                        category: 'React'
                    }
                ],
                
                // Contact Form
                form: {
                    name: '',
                    email: '',
                    subject: '',
                    message: ''
                },
                
                // Social Links
                socialLinks: [
                    { name: 'GitHub', url: 'https://github.com', icon: 'fab fa-github' },
                    { name: 'LinkedIn', url: 'https://linkedin.com', icon: 'fab fa-linkedin' },
                    { name: 'Twitter', url: 'https://twitter.com', icon: 'fab fa-twitter' },
                    { name: 'Instagram', url: 'https://instagram.com', icon: 'fab fa-instagram' }
                ]
            },
            computed: {
                filteredProjects() {
                    if (this.activeFilter === 'All') {
                        return this.projects
                    }
                    return this.projects.filter(project => 
                        project.technologies.includes(this.activeFilter) || 
                        project.category === this.activeFilter
                    )
                }
            },
            methods: {
                changePage(page) {
                    this.currentPage = page
                    this.isMenuOpen = false
                    window.scrollTo(0, 0)
                },
                toggleMenu() {
                    this.isMenuOpen = !this.isMenuOpen
                },
                toggleDarkMode() {
                    this.darkMode = !this.darkMode
                    document.body.classList.toggle('dark-mode', this.darkMode)
                },
                handleScroll() {
                    this.isScrolled = window.scrollY > 50
                },
                submitForm() {
                    // Here you would typically send the form data to a server
                    alert('Thank you for your message! I will get back to you soon.')
                    this.form = {
                        name: '',
                        email: '',
                        subject: '',
                        message: ''
                    }
                }
            },
            mounted() {
                window.addEventListener('scroll', this.handleScroll)
                
                // Check for saved theme preference or respect OS preference
                if (localStorage.getItem('darkMode') === 'true' || 
                    (window.matchMedia('(prefers-color-scheme: dark)').matches && !localStorage.getItem('darkMode'))) {
                    this.toggleDarkMode()
                }
            },
            beforeDestroy() {
                window.removeEventListener('scroll', this.handleScroll)
            }
        })
    </script>
</body>
</html>
