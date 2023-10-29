<template>
  <div>
      <div class="login-area">
          <div class="login-container">
              <div class="login-container-text">
                  <div class="login">Área de Login</div>
                  <div class="login-text">Faça login para acessar nosso super-aplicativo</div>
              </div> 
          </div>
      </div>
      <ui-button design="primary" label="Fazer login com a Huggy" @click="redirectToExternalLogin" />
  </div>
</template>

<script>
import uiButton from "@/components/uiButton.vue"
export default {
    name: 'login-view',

    components: { uiButton },

  
    methods: {
    redirectToExternalLogin() {
      // Token de acesso que você deseja passar para a página de login externa
        const tokenDeAcesso = "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUyMjA4ZGZhNjg5NTliODdmYmYzYTE1YTU2NzVjNzQ1ZDkzNzdhNjY2MTZhNTE3MWU3MGFmNzBiMGEzZGQxODc1MzUzZmVhMzNjOGNjODBjIn0.eyJhdWQiOiJBUFAtOWM5ZjgzYmMtNWY3My00OThmLTk3YzMtMzZkMTQ5MmQ4NGVmIiwianRpIjoiZTIyMDhkZmE2ODk1OWI4N2ZiZjNhMTVhNTY3NWM3NDVkOTM3N2E2NjYxNmE1MTcxZTcwYWY3MGIwYTNkZDE4NzUzNTNmZWEzM2M4Y2M4MGMiLCJpYXQiOjE2OTg1MDQwMDcsIm5iZiI6MTY5ODUwNDAwNywiZXhwIjoxNzE0MzE1MjA3LCJzdWIiOiIxMzQ0ODkiLCJzY29wZXMiOlsiaW5zdGFsbF9hcHAiLCJyZWFkX2FnZW50X3Byb2ZpbGUiXX0.USCxOcyd2x1mPLNXBLqKqzMKjX-kLTXFImQDrjhGume1grIKqDqtWLO8uFdUToGDx2FMdU3mGweIIcz_8WBwOgH9cB8jO1twxlINp9s5Ak_6sIiG10cA1pohxlIUf9X5CR1uI5CCh2R9oy1m2yU_VkVwFkxBM1e6XO-Xf1t_3mE";

      // URL da página de login externa com o token de acesso como parâmetro
      const urlDaPaginaDeLoginExterna = `https://www.huggy.app/?access_token=${tokenDeAcesso}&return=http://localhost:8080/atendimento`;

      // Redireciona o usuário para a página de login externa
      window.location.href = urlDaPaginaDeLoginExterna;
    }
  },
}
</script>

<style scoped lang="stylus">
.login
    color #2934A5 
    font-size 26px
    font-family IBM Plex Sans 
    font-weight 400
    line-height 46.80px
    word-wrap break-word
    &-container
      padding-bottom 48px
      flex-direction column 
      justify-content center 
      align-items center
      gap 64px 
      display inline-flex
      &-text
          flex-direction column 
          justify-content flex-start 
          align-items center
          display flex
    &-area
      width 100%
      height 100% 
      background white
      border-radius 2px 
      overflow hidden
      justify-content center 
      align-items center
      display inline-flex
    &-text
        color #46464A
        font-size 16px 
        font-family IBM Plex Sans 
        font-weight 400 
        line-height: 28.80px 
        word-wrap break-word

        
</style>