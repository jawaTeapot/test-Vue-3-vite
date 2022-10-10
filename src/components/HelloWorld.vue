<template>
  <section class="header">
    <div class="header__heading">Документы</div>
    <div class="header__buttons">
      <button class="header__buttons-bookmark btn">
        <img src="/vector.svg" alt="img" />
      </button>
      <button class="header__buttons-btn btn">
        <img src="/vector_2.svg" alt="img" /> Новый тип
      </button>
      <button class="header__buttons-btn btn">
        <img src="/vector_2.svg" alt="img" /> Новый документ
      </button>
    </div>
  </section>
  <section class="search">
    <div class="search__block">
      <img class="search__block-img" src="/vector_4.svg" alt="img" />
      <input
        class="search__input"
        type="text"
        placeholder="Поиск"
        v-model="search"
      />
    </div>
    <button class="search__btn btn" v-if="search" @click="search = ''">
      <img src="/vector_3.svg" alt="" />
    </button>
  </section>
  <section class="main">
    <draggable
      tag="ul"
      :list="filteredList"
      class="list-group"
      handle=".handle"
      item-key="name"
    >
      <template #item="{ element, index }">
        <div class="list-group">
          <Accordion>
            <template #top>
              <div class="accordion__top">
                <div class="accordion__top-block">
                  <button class="accordion__top-btn btn">
                    <img src="/vector_7.svg" alt="img" />
                  </button>
                  <div class="accordion__top-heading">
                    {{ element.name }}
                  </div>
                  <StatusColor :state="element.state" />
                  <div class="accordion__text">
                    {{ element.text }}
                  </div>
                </div>
                <AccordionButtons />
              </div>
            </template>
            <div class="accordion__list">
              <draggable
                tag="div"
                :list="element.children"
                item-key="name"
                group="elements"
              >
                <template #item="{ element, index }">
                  <div class="accordion__item">
                    <div class="accordion__item-block">
                      <div class="accordion__item-headline">
                        {{ element.name }}
                      </div>
                      <StatusColor :state="element.state" />
                      <div class="accordion__item-status">
                        {{ element.status }}
                      </div>
                      <div class="accordion__text">{{ element.text }}</div>
                    </div>
                    <AccordionButtons />
                  </div>
                </template>
              </draggable>
            </div>
          </Accordion>
        </div>
      </template>
    </draggable>
    <div class="elements">
      <div class="accordion__list">
        <draggable
          tag="div"
          :list="filteredItems"
          item-key="name"
          group="elements"
        >
          <template #item="{ element, index }">
            <div class="accordion__item">
              <div class="accordion__item-block">
                <div class="accordion__item-headline">{{ element.name }}</div>
                <StatusColor :state="element.state" />
                <div class="accordion__text">{{ element.text }}</div>
              </div>
              <AccordionButtons></AccordionButtons>
            </div>
          </template>
        </draggable>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from "vue";
import draggable from "vuedraggable";

import Accordion from "./Accordion.vue";
import AccordionButtons from "./AccordionButtons.vue";
import StatusColor from "./StatusColor.vue";

const list = ref([
  {
    name: "Обязательные для всех",
    text: "Документы, обязательные для всех сотрудников без исключения",
    state: "mandatory",
    children: [
      {
        name: "Паспорт",
        status: "Обязательный",
        text: "Для всех",
        state: "ellipse",
      },
      {
        name: "ИНН",
        status: "Обязательный",
        text: "Для всех",
      },
    ],
  },
  {
    name: "Обязательные для трудоустройства",
    text: "Документы, без которых невозможно трудоустройство человека на какую бы то ни было должность в компании вне зависимости от граж",
    children: [
      {
        name: "Трудовой договр",
        text: "",
        state: "contract",
      },
    ],
  },
  {
    name: "Специальные",
    text: "",
    children: [
      {
        name: "Мед. книжка",
        text: "",
      },
    ],
  },
]);
const items = ref([
  {
    name: "Тестовое задание кандидата",
    text: "Россия, Белоруссия, Украина, администратор филиала, повар-сушист, повар-пиццмейкер, повар горячего цеха",
  },
  {
    name: "Трудовой договор",
    text: "",
    state: "contract",
  },
  {
    name: "Мед. книжка",
    text: "",
  },
]);

const search = ref("");

const filteredList = computed(() => {
  return list.value.map((el) => {
    return {
      ...el,
      children: el.children.filter((ch) => {
        if (ch.name.toLowerCase().includes(search.value.toLowerCase())) {
          return ch;
        }
      }),
    };
  });
});

const filteredItems = computed(() => {
  return items.value.filter((el) => {
    return el.name.toLowerCase().includes(search.value.toLowerCase());
  });
});
</script>

<style lang="scss" scoped>
@import "../assets/variables.scss";
.header {
  margin-top: 38px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  &__heading {
    font-weight: 500;
    font-size: 22px;
    line-height: 24px;
    color: $primary-text;
  }
  &__buttons {
    display: flex;
    align-items: center;
    &-bookmark {
      width: 30px;
      height: 30px;
      justify-content: center;
      border: 1px solid $border-btn;
    }
    &-btn {
      margin-left: 10px;
      padding: 8px 20px 8px 10px;
      height: 30px;
      border: 1px solid $border-btn;
      img {
        margin-right: 10px;
      }
    }
  }
}
.search {
  margin-top: 23px;
  width: 565px;
  padding-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid $border;
  &:focus-within {
    border-bottom: 1px solid $border-bottom;
  }
  &__block {
    display: flex;
    align-items: center;
    &-img {
      margin-right: 12px;
    }
  }
  &__input {
    width: 500px;
    border: none;
    outline: none;
    font-weight: 400;
    font-size: 15px;
    line-height: 16px;
    color: $primary-text;
    &::placeholder {
      font-style: italic;
      font-weight: 400;
      font-size: 15px;
      line-height: 16px;
      color: $secondary-text;
    }
  }
  &__btn {
    width: 12px;
    height: 12px;
    justify-content: center;
  }
}
.main {
  margin-top: 19px;
}
.accordion {
  &__top {
    padding: 13px 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid $border;
    &-block {
      display: flex;
      align-items: center;
    }
    &-btn {
      margin-right: 14px;
      width: 22px;
      height: 22px;
      justify-content: center;
      border: 1px solid $border-btn;
    }
    &-heading {
      margin-right: 16px;
      font-weight: 500;
      font-size: 15px;
      line-height: 16px;
      color: $primary-text;
    }
  }
  &__text {
    font-weight: 400;
    font-size: 11px;
    line-height: 12px;
    color: $secondary-text;
  }
  &__list {
    margin-left: 16px;
  }
  &__item {
    padding: 10px 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid $border;
    &-block {
      display: flex;
      align-items: center;
    }
    &-headline {
      margin-right: 20px;
      font-weight: 400;
      font-size: 13px;
      line-height: 14px;
      color: $primary-text;
    }
    &-status {
      margin-right: 16px;
      font-weight: 400;
      font-size: 11px;
      line-height: 12px;
      color: $pink;
    }
  }
}
.elements {
  margin-top: 14px;
  width: 1190px;
  .accordion__list {
    margin-left: 0;
  }
}
</style>
