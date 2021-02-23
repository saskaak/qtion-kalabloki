<template>
  <div class="app">
    <div class="container">
      <div class="app__title">
        Qtion
        <br>
        kalabloki
      </div>

      <Message
        v-for="message in messages"
        :key="message.id"
        :message="message.message"
        :author="message.author"
        :time="message.time"
        class="app__message"
      />
    </div>
  </div>
</template>

<script>
import messages from '@/qtion-kalabloki.json';
import Message from '@/components/Message';

const images = {
  'FSJHB.png': require('@/assets/images/FSJHB.png'),
  'gyeNiP3.jpg': require('@/assets/images/gyeNiP3.jpg'),
  'JBXEN1P.jpg': require('@/assets/images/JBXEN1P.jpg'),
  'kuva1-2.jpg': require('@/assets/images/kuva1-2.jpg'),
  'kuva2-2.jpg': require('@/assets/images/kuva2-2.jpg'),
  'kuva3-2.jpg': require('@/assets/images/kuva3-2.jpg'),
  'kuva4-1.jpg': require('@/assets/images/kuva4-1.jpg'),
  'kuva5-1.jpg': require('@/assets/images/kuva5-1.jpg'),
  'kuva6-1.jpg': require('@/assets/images/kuva6-1.jpg'),
  'kuva7-1.jpg': require('@/assets/images/kuva7-1.jpg'),
  'kuva8-1.jpg': require('@/assets/images/kuva8-1.jpg'),
  'mTKx8TM.jpg': require('@/assets/images/mTKx8TM.jpg'),
};

const tags = {
  img: (size, originalUrl) => {
    const filename = originalUrl.split('/').pop().split('#')[0].split('?')[0]; // https://stackoverflow.com/a/36756650
    const url = images[filename] || originalUrl;
    return size
      ? `<img src="${url}" width="${size}">`
      : `<img src="${url}">`;
  },
  quote: (sourceId, body) => {
    const sourceMessage = messages.find((message) => message.id === parseInt(sourceId));
    return `<figure><figcaption>${sourceMessage.author}</figcaption><blockquote>${body}</blockquote></figure>`;
  },
  url: (url, body) => `<a href="${url}">${body}</a>`,
}

const messagesParsed = messages.map((message) => {
  const tagsOr = Object.keys(tags).join('|');
  const regex = new RegExp(`\\[(${tagsOr})=?(.*?)](.*?)\\[\\/\\1]`, 'gs');
  return {
    ...message,
    message: message.message.replaceAll(regex, (match, tag, ...args) => tags[tag](...args)),
    time: new Date(message.time * 1000).toLocaleString('fi-FI', {
      year: 'numeric',
      month: 'numeric',
      day: 'numeric',
      hour: '2-digit',
      minute: '2-digit',
    }),
  }
})

export default {
  name: 'App',
  components: {
    Message,
  },
  data() {
    return {
      messages: messagesParsed,
    }
  },
}
</script>

<style lang="scss">
@import "styles/definitions";

.app {
  margin: r(32) 0;

  @include breakpoint(S) {
    margin: r(64) 0;
  }
}

.app__title {
  margin-bottom: r(32);
  font-size: r(64);
  font-weight: 700;

  @include breakpoint(S) {
    margin-bottom: r(64);
    font-size: r(80);
  }
}

.app__message {
  & + & {
    margin-top: r(24);

    @include breakpoint(S) {
      margin-top: r(40);
    }
  }
}
</style>
