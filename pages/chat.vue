<template>
  <div class="c-wrap">
    <div class="c-chat" ref="block">
      <Message
        v-for="(m, i) in messages" :key="i"
        :name="m.name"
        :text="m.text"
        :owner="m.id === user.id"
      />
    </div>
    <div class="c-form">
      <ChatForm />
    </div>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import Message from '@/components/Message'
import ChatForm from '@/components/ChatForm'

export default {
  middleware: ['chat'],
  computed: mapState(['user', 'messages']),
  head() {
    return {
      title: `Комната ${this.user.room}`
    }
  },
  watch: {
    messages() {
      setTimeout(() => {
        this.$refs.block.scrollTop = this.$refs.block.scrollHeight
      },0)
    }
  },
  components: {
    Message,
    ChatForm
  }
}
</script>

<style lang="scss" scoped>
  .c{
    &-wrap{
      height: 100%;
      position: relative;
      overflow: hidden;
    }
    &-form{
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      padding: 10px;
      height: 90px;
      background: #212123;
    }
    &-chat{
      position: absolute;
      top: 0;
      right: 0;
      left: 0;
      bottom: 80px;
      padding: 1rem;
      overflow-y: auto;
    }
  }
</style>