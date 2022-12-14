<template lang="">
    <aside :class="`${is_expanded ? 'is-expanded' : ''}`">
       <div class="logo">
        <img src="../assets/coin_logo.png" alt="">
       </div>
       <div class="menu-toggle-wrap">
            <button class="menu-toggle" @click="ToggleMenu">
                <span class="material-icons material-icon--outlined">
                    keyboard_double_arrow_right
                    </span>
            </button>
       </div>
       <h3>Меню</h3>
       <div class="menu">
            <router-link class="button" to="/">
                <span class="material-icons">palette</span>
                <span class="text">Создание монеты</span>
            </router-link>
            <router-link class="button" to="/about">
                <span class="material-icons">receipt_long</span>
                <span class="text">Мои заказы</span>
            </router-link>
            
            
       </div>
    </aside>
</template>

<script setup>
    import {ref} from 'vue'

    const is_expanded = ref(false)

    const ToggleMenu = () => {
        is_expanded.value = !is_expanded.value

    }
</script>

<style lang="scss" scoped>
h3 {
  margin-bottom: 20px;
}
aside {
  display: flex;
  flex-direction: column;
  background-color: var(--dark);
  width: calc(2rem + 32px);
  min-height: 100vh;
  overflow: hidden;
  color: var(--light);
  padding: 1rem;
  transition: 0.2s ease-out;


  h3, .button .text {
    opacity: 0;
    transition: 0.3s ease-out;
   }
   .menu {
     margin: 0 -1rem;
     .button {
        display: flex;
        align-items: center;
        text-decoration: none;
        padding: 0.5rem 1rem;
        transition: 0.2s ease-out;

        .material-icons {
            font-size: 2rem;
            color: var(--light);
            transition: .2s ease-out;
        }
        .text {
            display: inline-block;
            margin-left: 20px;
            color: var(--light);
            transition: .2s ease-out;
        }
     }
   }
   .material-icon--outlined {
    transition: 0.2s ease-out;
    color: white;
    font-variation-settings: "FILL" 0, "wght" 800, "GRAD" 0, "opsz" 48;
    &:hover {
        color: var(--primary);
        transform: translateX(0.5rem);
    }
}
  &.is-expanded {
    width: var(--sidebar-width);
    .menu-toggle-wrap {
        top: -3rem;
        .menu-toggle {
            transition: 0.2s ease-out;
            transform: rotate(-180deg);
        }
    }
    h3, .button .text {
        opacity: 1;
       }
  }

  .logo {
    margin-bottom: 1rem;

    img {
      width: 2rem;
    }
  }


  .menu-toggle-wrap {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 1rem;
    position: relative;
    top: 0;
    transition: 0.2s ease-out;
  }

  @media (max-width: 768px) {
    position: fixed;
    z-index: 99;
  }
}
</style>