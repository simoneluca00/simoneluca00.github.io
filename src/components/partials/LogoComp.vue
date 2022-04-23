<template>
    <div id="logo">
      <a href="#">
        <span>Boolflix</span>
      </a>
    </div>
</template>

<script>

export default {
  name: 'LogoComp',

}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Monoton&display=swap');
@import '../../style/global.scss';

    #logo {
      a {
        text-decoration: none;
      }

      span {
        align-self: flex-end;
        color: $primary-red;
        font-size: 2.8em;
        font-family: 'Monoton', cursive;      
      }
    }
</style>