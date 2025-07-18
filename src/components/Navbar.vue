<template>
  <nav class="navbar navbar-expand-lg sticky-top shadow-sm navbar-dark">
    <div class="container">
      <div class="navbar-brand logo">
        <i class="fa-brands fa-slack" style="color: #B197FC;"></i>
        <router-link to="/" class="main-logo">Invela</router-link>
      </div>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown"
        aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse justify-content-center align-items-center" id="navbarNavDropdown">
        <ul class="navbar-nav w-100 ms-lg-5 justify-content-center align-items-center gap-4">
          <li class="nav-item">
            <router-link to="/" exact-active-class="active-link" class="nav-link fw-medium">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/Services" exact-active-class="active-link" class="nav-link fw-medium">Services</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/About" exact-active-class="active-link" class="nav-link fw-medium">About</router-link>
          </li>
          <li class="nav-item dropdown" @mouseleave="closeDropdown">
            <a class="nav-link fw-medium" href="#" role="button" @click.prevent="toggleDropdown"
              :aria-expanded="showDropdown">
              Contact
              <span :class="['dropdown-arrow', { rotated: showDropdown }]">
                <i class="fas fa-chevron-down"></i>
              </span>
            </a>
            <transition name="dropdown-fade">
              <ul v-show="showDropdown" class="dropdown-menu text-lg-start p-2"
                style="display: block; min-width: 160px">
                <li>
                  <router-link to="/SignIn" class="dropdown-item rounded-2">SignIn</router-link>
                </li>
                <li>
                  <router-link to="/Contact" class="dropdown-item rounded-2 mt-1">Contact</router-link>
                </li>
              </ul>
            </transition>
          </li>
          <li class="nav-item ms-lg-auto">
            <div class="hero-buttons">
              <button class="btn btn-outline">
                <i class="fas fa-play-circle"></i>
                <router-link to="/Login" class="dropdown-item">Login</router-link>
              </button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
const showDropdown = ref(false);

function toggleDropdown() {
  showDropdown.value = !showDropdown.value;
}

function closeDropdown() {
  showDropdown.value = false;
}

// Close dropdown on click outside or ESC key
function handleClickOutside(event) {
  const dropdown = document.querySelector(".nav-item.dropdown");
  if (dropdown && !dropdown.contains(event.target)) {
    closeDropdown();
  }
}
function handleEsc(event) {
  if (event.key === "Escape") closeDropdown();
}

onMounted(() => {
  document.addEventListener("mousedown", handleClickOutside);
  document.addEventListener("keydown", handleEsc);
});
onBeforeUnmount(() => {
  document.removeEventListener("mousedown", handleClickOutside);
  document.removeEventListener("keydown", handleEsc);
});
</script>

<style scoped>
/* Change background color of toggler icon */
.navbar-toggler-icon {
  background-image: url("data:image/svg+xml;charset=utf8,%3Csvg viewBox='0 0 30 30' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath stroke='blue' stroke-width='2' stroke-linecap='round' stroke-miterlimit='10' d='M4 7h22M4 15h22M4 23h22'/%3E%3C/svg%3E");
  color: 3px solid var(--primary);
}

.navbar {
  animation: slideDown 0.7s ease forwards;
  background-color: rgba(0, 0, 0, 0.916);

  & .navbar-nav {
    font-size: 1.13rem;

    & .nav-item > .nav-link {
      color: rgb(121, 103, 255) !important;
    }
  }
}

.btn {
  margin: 5px 0 5px 0;
  padding: 10px 20px;
  border-radius: var(--radius);
  font-weight: 500;
  cursor: pointer;
  transition: var(--transition);
  border: none;
  font-size: 1rem;
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.btn-primary {
  background: var(--primary);
  color: white;
  box-shadow: 0 4px 6px rgba(67, 97, 238, 0.3);
}

.btn-primary:hover {
  background: var(--secondary);
  transform: translateY(-3px);
  box-shadow: 0 10px 15px rgba(67, 97, 238, 0.4);
}

.btn-outline {
  background: transparent;
  border: 2px solid var(--primary);
  color: var(--primary);
}

.btn-outline:hover {
  background: var(--primary);
  color: white;
  transform: translateY(-3px);
}

.hero-buttons {
  display: flex;
  gap: 10px;
}

.dropdown-fade-enter-active,
.dropdown-fade-leave-active {
  transition: opacity 0.25s, transform 0.25s;
}

.dropdown-fade-enter-from,
.dropdown-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px) scaleY(0.95);
}

.dropdown-fade-enter-to,
.dropdown-fade-leave-from {
  opacity: 1;
  transform: translateY(0) scaleY(1);
}

/* Responsive dropdown menu */
.dropdown-menu {
  margin-top: 5px !important;
  border-radius: var(--radius);
  min-width: 180px;
  max-width: 90vw;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
  left: 0;
  right: auto;
  position: absolute;
  z-index: 1000;
  background: #fff;
  top: 100%;
  transform-origin: top;
  /* Animation handled by transition */
}

@media (max-width: 991.98px) {
  .btn {
    padding: 10px 90px;
    margin-top: -3px;
  }

  .navbar-nav {
    flex-direction: row !important;
    flex-wrap: wrap;
    gap: 1.8rem !important;
    width: 100%;
    align-items: stretch !important;
  }

  .hero-buttons {
    justify-content: center;
    width: 100%;
  }

  .dropdown-menu {
    position: static !important;
    width: 100%;
    min-width: unset;
    box-shadow: none;
    background: #fff;
    left: 0;
    right: 0;
    top: auto;
  }
}

.active-link {
  border-bottom: 2px solid #ffffff;
}

.logo {
  font-size: 1.8rem;
  font-weight: 700;
  margin-left: 15px;
  display: flex;
  align-items: center;
  gap: 10px;
  & .main-logo {
    text-decoration: none;
  }
}

.dropdown-arrow {
  display: inline-block;
  margin-left: 6px;
  transition: transform 0.3s cubic-bezier(0.4, 2, 0.6, 1);
}

.dropdown-arrow.rotated {
  transform: rotate(180deg);
}

@keyframes slideDown {
  from {
    transform: translateY(-100%);
  }

  to {
    transform: translateY(0);
  }
}
</style>
