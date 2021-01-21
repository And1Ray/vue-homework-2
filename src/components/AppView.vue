<template>
  <div class="card card-w70">
    <template v-for="block in blocks" :key="block">
      <app-title
        v-if="block.type === 'title'"
      >{{ block.content }}
      </app-title>

      <app-subtitle
        v-else-if="block.type === 'subtitle'"
      >{{ block.content }}
      </app-subtitle>

      <app-avatar
        class="avatar"
        :link="block.content"
        v-else-if="block.type === 'avatar'"
      ></app-avatar>

      <app-text
        v-else-if="block.type === 'text'"
      >{{ block.content }}
      </app-text>

    </template>

    <h3 v-if="getDefault">Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>
import AppTitle from '@/components/AppTitle'
import AppSubtitle from '@/components/AppSubtitle'
import AppText from '@/components/AppText'
import AppAvatar from '@/components/AppAvatar'

export default {
  props: {
    blocks: Array
  },
  computed: {
    getDefault () {
      return this.blocks.length <= 0
    }
  },
  components: { AppTitle, AppSubtitle, AppText, AppAvatar }
}
</script>
