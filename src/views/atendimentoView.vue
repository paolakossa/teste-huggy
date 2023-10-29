<template>
  <div class="body-container">
    <div class="body-container-header">
        <div class="body-container-header-message">
            <div class="body-container-header-message-text">Minhas mensagens</div>
        </div>
        <div class="container-image">
            <div class="container-image-header">
                <img class="container-image-property" :src="imagePath"/>
                <div class="container-text">
                    <div class="container-text-header">
                        <div class="conatiner-text-property">Agostinho Carrara</div>
                    </div>
                    <div class="container-message">
                        <div v-if="chatMessages.length > 0" class="container-message-property"> {{ chatMessages[0].text }}</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div class="body-container-context" >
        <div class="container-name">
            <div class="container-name-image">
                <img class="container-name-image-property" :src="imagePathSmall" />
                <div class="container-name-property">Agostinho Carrara</div>
            </div>
        </div>
        <div class="body-container-card" v-for="message in chatMessages" :key="message.id">
            <div class="body-container-card">
                <div class="body-container-card-background">
                    <div class="container-card-text">
                        <div class="container-card-text-background">
                            <div :class="message.senderType === 'agent' ? 'container-card-text-background-color-agent' : 'container-card-text-background-color'">
                                <div class="container-card-message">
                                    <div :class="message.senderType === 'agent' ? 'container-card-message-property-agent' : 'container-card-message-property'">{{ message.text }}</div>
                                </div>
                            </div>
                            <div class="container-card-time">
                                <div class="container-card-time-property">{{ formatDateTime(message.sendAt) }}</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="body-container-components">
            <ui-text-area v-model="newMessageText" placeholder="Escreva sua mensagem..."/>
            <div class="container-button">
                <ui-button class="sucess" label="Enviar" @click="reabrirChat"/>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import uiButton from "@/components/uiButton.vue"
import uiTextArea from "@/components/uiTextArea.vue"
import axios from "axios"
export default {
    name: 'atendimento-view',

    components: { uiButton, uiTextArea },

    data() {
      return {
        imagePath: require('@/assets/size=bigagostinho.svg'),
        imagePathSmall: require('@/assets/size=small.svg'),
        chatMessages: [],
        newMessageText: "",
      }
    },

    mounted() {
        this.getMessages()
    },

    methods: {
        formatDateTime(dateTime) {
            const date = new Date(dateTime);
            return date.toLocaleTimeString("pt-BR", { hour: "2-digit", minute: "2-digit" })
        },
        async getMessages() {
            const accessToken = "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUyMjA4ZGZhNjg5NTliODdmYmYzYTE1YTU2NzVjNzQ1ZDkzNzdhNjY2MTZhNTE3MWU3MGFmNzBiMGEzZGQxODc1MzUzZmVhMzNjOGNjODBjIn0.eyJhdWQiOiJBUFAtOWM5ZjgzYmMtNWY3My00OThmLTk3YzMtMzZkMTQ5MmQ4NGVmIiwianRpIjoiZTIyMDhkZmE2ODk1OWI4N2ZiZjNhMTVhNTY3NWM3NDVkOTM3N2E2NjYxNmE1MTcxZTcwYWY3MGIwYTNkZDE4NzUzNTNmZWEzM2M4Y2M4MGMiLCJpYXQiOjE2OTg1MDQwMDcsIm5iZiI6MTY5ODUwNDAwNywiZXhwIjoxNzE0MzE1MjA3LCJzdWIiOiIxMzQ0ODkiLCJzY29wZXMiOlsiaW5zdGFsbF9hcHAiLCJyZWFkX2FnZW50X3Byb2ZpbGUiXX0.USCxOcyd2x1mPLNXBLqKqzMKjX-kLTXFImQDrjhGume1grIKqDqtWLO8uFdUToGDx2FMdU3mGweIIcz_8WBwOgH9cB8jO1twxlINp9s5Ak_6sIiG10cA1pohxlIUf9X5CR1uI5CCh2R9oy1m2yU_VkVwFkxBM1e6XO-Xf1t_3mE"

        const config = {
            headers: {
                Authorization: `Bearer ${accessToken}`
            }
        }
        await axios
            .get("https://api.huggy.app/v3/chats/191724354/messages", config)
            .then(response => {
                this.chatMessages = response.data
            })
            .catch(error => {
                console.error("Erro na requisição GET:", error)
            });
        },
        async enviarMensagem() {
            const chatId = 191724354
            const token = "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUyMjA4ZGZhNjg5NTliODdmYmYzYTE1YTU2NzVjNzQ1ZDkzNzdhNjY2MTZhNTE3MWU3MGFmNzBiMGEzZGQxODc1MzUzZmVhMzNjOGNjODBjIn0.eyJhdWQiOiJBUFAtOWM5ZjgzYmMtNWY3My00OThmLTk3YzMtMzZkMTQ5MmQ4NGVmIiwianRpIjoiZTIyMDhkZmE2ODk1OWI4N2ZiZjNhMTVhNTY3NWM3NDVkOTM3N2E2NjYxNmE1MTcxZTcwYWY3MGIwYTNkZDE4NzUzNTNmZWEzM2M4Y2M4MGMiLCJpYXQiOjE2OTg1MDQwMDcsIm5iZiI6MTY5ODUwNDAwNywiZXhwIjoxNzE0MzE1MjA3LCJzdWIiOiIxMzQ0ODkiLCJzY29wZXMiOlsiaW5zdGFsbF9hcHAiLCJyZWFkX2FnZW50X3Byb2ZpbGUiXX0.USCxOcyd2x1mPLNXBLqKqzMKjX-kLTXFImQDrjhGume1grIKqDqtWLO8uFdUToGDx2FMdU3mGweIIcz_8WBwOgH9cB8jO1twxlINp9s5Ak_6sIiG10cA1pohxlIUf9X5CR1uI5CCh2R9oy1m2yU_VkVwFkxBM1e6XO-Xf1t_3mE"
            

            const mensagem = {
            text:  this.newMessageText,
            file: "https://c.pzw.io/img/avatar-user-boy.jpg",
            isInternal: false,
            };

            try {
             
            const response = await axios.post(
                `https://api.huggy.app/v3/chats/${chatId}/messages`,
                mensagem,
                {
                headers: {
                    Authorization: `Bearer ${token}`,
                },
                }
            );
            this.chatMessages.unshift(response.data)
            this.newMessageText = "";
            } catch (error) {
            console.error("Erro ao enviar a mensagem:", error)
            }
        },
        async reabrirChat() {
            const chatId = 191724354
            const token = "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUyMjA4ZGZhNjg5NTliODdmYmYzYTE1YTU2NzVjNzQ1ZDkzNzdhNjY2MTZhNTE3MWU3MGFmNzBiMGEzZGQxODc1MzUzZmVhMzNjOGNjODBjIn0.eyJhdWQiOiJBUFAtOWM5ZjgzYmMtNWY3My00OThmLTk3YzMtMzZkMTQ5MmQ4NGVmIiwianRpIjoiZTIyMDhkZmE2ODk1OWI4N2ZiZjNhMTVhNTY3NWM3NDVkOTM3N2E2NjYxNmE1MTcxZTcwYWY3MGIwYTNkZDE4NzUzNTNmZWEzM2M4Y2M4MGMiLCJpYXQiOjE2OTg1MDQwMDcsIm5iZiI6MTY5ODUwNDAwNywiZXhwIjoxNzE0MzE1MjA3LCJzdWIiOiIxMzQ0ODkiLCJzY29wZXMiOlsiaW5zdGFsbF9hcHAiLCJyZWFkX2FnZW50X3Byb2ZpbGUiXX0.USCxOcyd2x1mPLNXBLqKqzMKjX-kLTXFImQDrjhGume1grIKqDqtWLO8uFdUToGDx2FMdU3mGweIIcz_8WBwOgH9cB8jO1twxlINp9s5Ak_6sIiG10cA1pohxlIUf9X5CR1uI5CCh2R9oy1m2yU_VkVwFkxBM1e6XO-Xf1t_3mE"


            try {
                const response = await axios.put(
                    `https://api.huggy.app/v3/chats/${chatId}/reopen`,
                    {},
                    {
                        headers: {
                        Authorization: `Bearer ${token}`,
                        },
                    }
                )
                this.enviarMensagem();
            } catch (error) {
                console.error("Erro ao reabrir o chat:", error)
            }
        },
    }
    
}
</script>

<style scoped lang="stylus">
.body-container
  width: 100%
  height: 100% 
  background: white
  border-radius: 2px 
  justify-content: flex-start
  align-items: flex-start 
  display: inline-flex
  &-header
    width: 300px 
    align-self: stretch
    padding-left: 8px 
    padding-right: 8px 
    
    border-right: 1px #F0F0F2 solid 
    flex-direction: column 
    justify-content: flex-start 
    align-items: flex-start 
    display: inline-flex
    &-message
      align-self: stretch 
      height: 64px
      padding-left: 16px
      padding-right: 16px
      border-bottom: 1px #E8E8EB solid
      justify-content: flex-start
      align-items: center
      display: inline-flex
      &-text
        color: #2934A5
        font-size: 20px
        font-family: IBM Plex Sans 
        font-weight: 500 
        line-height: 36px 
        word-wrap: break-word
  .container-image
    align-self: stretch
    height: 282px 
    padding-top: 8px
    padding-bottom: 8px 
    flex-direction: column
    justify-content: flex-start 
    align-items: flex-start 
    gap: 4px 
    display: flex
    &-header
      align-self: stretch
      height: 86px
      padding-left: 8px
      padding-right: 8px 
      background: #EEF0FC 
      border-radius: 4px 
      overflow: hidden
      justify-content: flex-start 
      align-items: center 
      gap: 12px
      display: inline-flex
    &-property
      width: 52px 
      height: 52px
      border-radius: 8px 
      border: 1px #E8E8EB solid
  .container-text
    flex: 1 1 0
    align-self: stretch
    flex-direction: column 
    justify-content: center 
    align-items: flex-start 
    display: inline-flex
    &-header
      align-self: stretch
      justify-content: flex-start
      align-items: center
      display: inline-flex
    &-property
      flex: 1 1 0 
      height: 29px 
      color: #2934A5 
      font-size: 16px
      font-family: IBM Plex Sans 
      font-weight: 500 
      line-height: 25.60px 
      word-wrap: break-word
  .container-message
    align-self: stretch 
    height: 20px 
    justify-content: flex-start 
    align-items: center 
    display: inline-flex
    &-property
      flex: 1 1 0
      align-self: stretch
      color: #46464A
      font-size: 14px
      font-family: IBM Plex Sans 
      font-weight: 400
      line-height: 25.20px
      word-wrap: break-word
      margin-right: 85px
.body-container-context
    flex: 1 1 0 
    height: 788px
    background: white
    flex-direction: column
    justify-content: flex-start
    align-items: flex-start
    display: inline-flex
.container-name
    align-self: stretch 
    height: 64px 
    padding-left: 16px
    padding-right: 16px
    
    box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.04) 
    flex-direction: column 
    justify-content: center 
    align-items: flex-start 
    display: flex
    &-image
        justify-content: flex-start 
        align-items: center 
        gap: 8px
        display: inline-flex
        &-property
            height: 40px 
            border-radius: 8px 
            border: 1px #E8E8EB solid
    &-property
        color: #141316 
        font-size: 16px 
        font-family: IBM Plex Sans 
        font-weight: 500
        line-height: 25.60px 
        word-wrap: break-word
.body-container-card
    align-self: stretch
    flex: 1 1 0 
    flex-direction: column 
    justify-content: flex-start 
    align-items: flex-start 
    display: flex
    &-background
        align-self: stretch 
        flex: 1 1 0
        padding: 16px 
        background: #F6F6F8 
        justify-content: center 
        align-items: flex-end 
        display: inline-flex
.container-card-text
    flex: 1 1 0 
    align-self: stretch 
    flex-direction: column 
    justify-content: flex-end 
    align-items: center 
    display: inline-flex
    &-background
        align-self: stretch 
        height: 124px 
        padding-top: 8px 
        padding-bottom: 8px 
        padding-left: 16px 
        flex-direction: column 
        justify-content: center 
        align-items: flex-end 
        display: flex
        &-color
            align-self: stretch 
            padding-left: 20px 
            padding-right: 20px 
            padding-top: 14px
            padding-bottom: 14px
            background: #374FC9 
            border-top-left-radius: 6px
            border-top-right-radius: 6px 
            border-bottom-right-radius: 2px 
            border-bottom-left-radius: 6px 
            border: 1px #374FC9 solid 
            justify-content: flex-start 
            align-items: flex-start 
            gap: 10px 
            display: inline-flex
            &-agent
                background: #fff

    .container-card-message
        flex: 1 1 0 
        height: 58px 
        justify-content: flex-start 
        align-items: flex-start 
        display: flex
        &-property
            flex: 1 1 0
            color: white 
            font-size: 16px 
            font-family: IBM Plex Sans 
            font-weight: 400 
            line-height: 28.80px 
            word-wrap: break-word
            &-agent
                flex: 1 1 0
                font-size: 16px 
                font-family: IBM Plex Sans 
                font-weight: 400 
                line-height: 28.80px 
                word-wrap: break-word
                color: #232326
    .container-card-time
        justify-content: flex-start 
        align-items: flex-start 
        display: inline-flex
        &-property
            color: #232326 
            font-size: 12px 
            font-family: IBM Plex Sans 
            font-weight: 400 
            line-height: 21.60px
            word-wrap: break-word
    .container-button
        align-self: stretch 
        padding-left: 24px 
        padding-right: 24px 
        padding-top: 12px 
        padding-bottom: 12px 
        background: #DCDCE1 
        border-radius: 8px 
        overflow: hidden 
        justify-content: center 
        align-items: center 
        display: inline-flex
.body-container-components
    align-self: stretch 
    height: 169px 
    padding-left: 24px 
    padding-right: 24px 
    padding-top: 16px 
    padding-bottom: 16px
    box-shadow: 0px -1px 6px rgba(0, 0, 0, 0.03) 
    flex-direction: column 
    justify-content: flex-start 
    align-items: center 
    gap: 8px 
    display: flex

</style>