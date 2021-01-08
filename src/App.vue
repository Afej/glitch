<template>
  <div v-if="loading">
    <div class="spinner-container">
      <div class="spinner"></div>
    </div>
  </div>
  <div v-else class="container">
    <h1 class="name">{{ name }}</h1>

    <main>
      <div class="image-container">
        <img src="./assets/main-img.jpg" alt="main-image" class="main-image" />
      </div>

      <nav>
        <ul class="nav-items">
          <li class="nav-item"><a href="#">Home</a></li>
          <li class="nav-item"><a href="#">About</a></li>
          <li class="nav-item">
            <div class="nav-image">
              <img src="./assets/nav-img.png" alt="nav-image" />
            </div>
          </li>
          <li class="nav-item"><a href="#">Gallery</a></li>
          <li class="nav-item"><a href="#">Contact</a></li>
        </ul>
      </nav>
      <aside>
        <ul class="social-links">
          <li class="social-link-item">
            <a :href="social_media.instagram" target="_blank">
              <i class="fab fa-instagram fa-3x social-icon"></i>
            </a>
          </li>
          <li class="social-link-item">
            <a :href="social_media.twitter" target="_blank">
              <i class="fab fa-twitter-square fa-3x social-icon"></i>
            </a>
          </li>
          <li class="social-link-item">
            <a :href="social_media.snapchat" target="_blank">
              <i class="fab fa-snapchat-square fa-3x social-icon"></i>
            </a>
          </li>
          <li class="social-link-item">
            <a :href="social_media.email" target="_blank">
              <i class="fas fa-envelope-square fa-3x social-icon"></i>
            </a>
          </li>
        </ul>
      </aside>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      name: "",
      social_media: {
        email: "mailto:",
        instagram: "https://instagram.com/",
        snapchat: "https://snapchat.com/",
        twitter: "https://twitter.com/",
      },
      loading: true,
    };
  },
  created() {
    axios
      .get("https://hirng-x2021.glitch.me/api")
      .then((res) => {
        this.name = res.data.name;
        for (const [aKey, aValue] of Object.entries(res.data.social_media)) {
          Object.entries(this.social_media).map(([bKey, bValue]) => {
            if (aKey === bKey) {
              return `${bKey}: ${bValue}${aValue}`;
            }
          });
        }

        this.loading = false;
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body {
  font-family: "Noto Sans JP", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  background: rgb(189, 15, 77);
  background: linear-gradient(
    90deg,
    rgba(189, 15, 77, 1) 50%,
    rgba(203, 41, 100, 1) 50%
  );
  background-repeat: no-repeat;
  background-size: cover;
  height: 100%;
  min-height: 100vh;
  line-height: 1.5;
}

ul {
  list-style: none;
}

a {
  text-decoration: none;
  color: #fff;
  cursor: pointer;
}

.spinner-container {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.spinner {
  display: inline-block;
  width: 50px;
  height: 50px;
  border: 3px solid rgba(195, 195, 195, 0.6);
  border-radius: 50%;
  border-top-color: #636767;
  animation: spin 1s ease-in-out infinite;
  -webkit-animation: spin 1s ease-in-out infinite;
}

@keyframes spin {
  to {
    -webkit-transform: rotate(360deg);
  }
}
@-webkit-keyframes spin {
  to {
    -webkit-transform: rotate(360deg);
  }
}

.container {
  margin: 0 auto;
  padding: 2rem;
  max-width: 800px;
}

.name {
  letter-spacing: 10px;
  font-weight: 200;
  margin-top: 1rem;
}

main {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.image-container {
  width: 500px;
  height: 500px;
  margin: 2rem auto;
}

.main-image {
  width: 100%;
  height: 100%;
}

aside {
  right: 30px;
  color: #fff;
  position: fixed;
  top: 35%;
}

.social-link-item {
  margin: 1rem 0;
}

.nav-items {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-bottom: 50px;
}

.nav-item {
  font-size: 1.2rem;
  letter-spacing: 5px;
  text-transform: uppercase;
  width: 120px;
}

.nav-image {
  width: 120px;
  height: 120px;
}

.nav-image img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
}

@media (max-width: 768px) {
  .name {
    font-size: 0.9rem;
  }

  .image-container {
    width: 350px;
    height: 350px;
  }

  .nav-items {
    flex-direction: column;
  }

  .nav-item {
    margin: 0.5rem 0;
    font-size: 1rem;
  }

  .nav-image {
    width: 120px;
    height: 120px;
  }

  aside {
    right: 15px;
    bottom: 0;
    top: 60%;
  }

  .social-icon {
    font-size: 2em;
  }
}

@media (max-width: 500px) {
  .image-container {
    width: 250px;
    height: 250px;
  }
}
</style>
