<!-- eslint-disable vue/v-on-event-hyphenation -->
<!-- eslint-disable vue/no-v-html -->
<template>
  <section class="s-admin">
    <div class="s-admin__container l-wide">
      <h1 class="s-admin__title s-title">Админ панель</h1>
      <div class="s-admin__block">
        <div class="s-admin__main _border">
          <h2 class="s-admin__subtitle">Основная информация:</h2>
          <div class="s-admin__row">
            <h3 class="s-admin__row-title">Название:</h3>
            <input v-model="itemTitle" class="s-admin__input" placeholder="Заголовок статьи" />
          </div>
          <div class="s-admin__row">
            <h3 class="s-admin__row-title">Основной текст:</h3>
            <s-editor
              :item-content="itemContent"
              :create-or-update="createOrUpdate"
              @setNewArticle="createArticle"
              @updateArticle="updateArticle"
            />
          </div>
        </div>
        <div class="s-admin__aside _border">
          <div class="s-admin__box _content">
            <h2 class="s-admin__subtitle">Все статьи:</h2>
            <div class="s-admin__box-items">
              <div v-for="item in allArticles" :key="item.id" class="s-admin__box-item">
                <h3 class="s-admin__box-item-title">{{ item.data.title }} / {{ item.data.id }}</h3>
                <div class="s-admin__box-item-logic">
                  <div class="s-admin__box-item-action _green" @click="editingArticle(item.id)">Р</div>
                  <div class="s-admin__box-item-action _brown">С</div>
                  <div class="s-admin__box-item-action _red">У</div>
                </div>
              </div>
            </div>
          </div>
          <div class="s-admin__box">
            <button class="s-admin__button" @click="getAllArticles">загрузить</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script setup>
// import getArticles from '~/api/getArticles';
import setNewArticle from '~/api/setNewArticle';
const allArticles = ref([]);
const currentArticle = ref([]);
const createOrUpdate = ref(true);

const itemTitle = ref('');
const itemContent = ref('');

const createArticle = async (content) => {
  await setNewArticle(content, itemTitle.value);
};
const editingArticle = (id) => {
  currentArticle.value = allArticles.value.find((item) => item.id === id);
  itemTitle.value = currentArticle.value.data.title;
  itemContent.value = currentArticle.value.data.content;
};

const updateArticle = () => {
  console.log('аммвы');
};

async function getAllArticles() {
  // const response = await getArticles();
  const response = [
    {
      data: {
        createAt: {
          seconds: 1706107660,
          nanoseconds: 186000010,
        },
        title: 'Первая статья',
        visible: true,
        content: '<p>тадыaaaaaaaaaaaaaщь</p><p>тыщ</p>',
        id: 9008485,
      },
      id: '9008485',
    },
    {
      data: {
        createAt: {
          seconds: 1706107640,
          nanoseconds: 186000020,
        },
        title: 'dvsdvsdv статья',
        visible: true,
        content: '<p>111111</p><p>тыщ</p>',
        id: 9008486,
      },
      id: '9008486',
    },
    {
      data: {
        createAt: {
          seconds: 1706107690,
          nanoseconds: 186000060,
        },
        title: 'Nhtnmz статья',
        visible: true,
        content: '<p>sss</p><p>тыщ</p>',
        id: 9008487,
      },
      id: '9008487',
    },
  ];
  allArticles.value = response.sort((a, b) => a.data.createAt - b.data.createAt);
}
onMounted(() => {
  // getAllArticles();
});
</script>

<style lang="scss">
@import './s-admin.scss';
</style>
