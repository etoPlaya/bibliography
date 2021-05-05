<template>
  <header>
    <div class="content">
      <p>Библиография — это сервис составления библиографического описания различных источников информации.</p>

      <LogoIcon/>

      <a href="https://goldcarrot.ru/" class="developer" target="_blank">
        <span>Сделано в </span>
        <GcIcon/>
      </a>
    </div>
  </header>	
</template>

<script>
import LogoIcon from '@/assets/ui/logo.svg';
import GcIcon from '@/assets/ui/gc.svg';

export default {
  components: {
    GcIcon,
    LogoIcon,
  },
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';

header {
  .content {
    @include mobile {
      display: flex;
      align-content: center;
      justify-content: space-between;
      
      padding: 30px 20px 10px 20px !important;
    }
  }
}

p {
  font-size: 12px;
  line-height: 15px;

  color: rgba(255, 255, 255, 0.33);

  @include mobile {
    display: none;
  }

  & ~ svg {
    display: block;
    margin-top: 10px;

    @include mobile {
      margin-top: 0;
    }
  }
}

a {
  position: absolute;
  right: 40px;
  top: 13px;

  font-size: 12px;
  line-height: 15px;
  color: #9092A8;

  transition: 250ms ease all;

  &:hover {
    color: gold;
    svg {
      fill: gold;
      opacity: 1;
    }
  }

  @include mobile {
    position: static;
  }
  
  span {
    @include mobile {
      display: none;
    }
  }

  svg {
    fill: white;
    opacity: 0.3;

    transition: 250ms ease all;
  }
}
</style>