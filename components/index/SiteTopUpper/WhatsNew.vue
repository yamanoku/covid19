<template>
  <div class="WhatsNew">
    <div class="WhatsNew-heading">
      <h3 class="WhatsNew-title">
        <v-icon size="2.4rem" class="WhatsNew-title-icon">
          {{ mdiInformation }}
        </v-icon>
        {{ $t('最新のお知らせ') }}
      </h3>
      <ul class="WhatsNew-linkGroup">
        <li>
          <app-link
            class="WhatsNew-linkButton"
            to="https://www.fukushihoken.metro.tokyo.lg.jp/iryo/kansen/coronavaccine/index.html"
          >
            <span class="WhatsNew-linkButton-inner">
              <vaccine-icon
                class="WhatsNew-linkButton-icon"
                aria-hidden="true"
              />
              {{ $t('ワクチン情報') }}
            </span>
          </app-link>
        </li>
        <li>
          <app-link
            class="WhatsNew-linkButton"
            to="https://www.fukushihoken.metro.tokyo.lg.jp/iryo/kansen/screening.html"
          >
            <span class="WhatsNew-linkButton-inner">
              <covid-icon class="WhatsNew-linkButton-icon" aria-hidden="true" />
              {{ $t('変異株情報') }}
            </span>
          </app-link>
        </li>
        <li>
          <app-link
            class="WhatsNew-linkButton"
            to="https://www.fukushihoken.metro.tokyo.lg.jp/iryo/kansen/kensa/index.html"
          >
            <span class="WhatsNew-linkButton-inner">
              <v-icon size="1em" class="WhatsNew-linkButton-v-icon">
                {{ mdiClipboardText }}
              </v-icon>
              {{ $t('検査情報') }}
            </span>
          </app-link>
        </li>
      </ul>
    </div>
    <ul class="WhatsNew-list">
      <li v-for="(item, i) in items" :key="i" class="WhatsNew-list-item">
        <app-link :to="item.url" class="WhatsNew-list-item-anchor">
          <time
            class="WhatsNew-list-item-anchor-time px-2"
            :datetime="formattedDate(item.date)"
          >
            {{ formattedDateForDisplay(item.date) }}
          </time>
          <span class="WhatsNew-list-item-anchor-link">
            {{ item.text }}
          </span>
        </app-link>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { mdiClipboardText, mdiInformation } from '@mdi/js'
import Vue from 'vue'

import AppLink from '@/components/_shared/AppLink.vue'
import CovidIcon from '@/static/covid.svg'
import VaccineIcon from '@/static/vaccine.svg'
import { convertDateToISO8601Format } from '@/utils/formatDate'

export default Vue.extend({
  components: {
    AppLink,
    VaccineIcon,
    CovidIcon,
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      mdiClipboardText,
      mdiInformation,
    }
  },
  methods: {
    formattedDate(dateString: string) {
      return convertDateToISO8601Format(dateString)
    },
    formattedDateForDisplay(dateString: string) {
      return this.$d(new Date(dateString), 'date')
    },
  },
})
</script>

<style lang="scss">
.WhatsNew {
  @include card-container();

  padding: 5px 18px;
  margin-bottom: 10px;

  .WhatsNew-heading {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    margin-bottom: 8px;

    .WhatsNew-title {
      display: flex;
      align-items: center;
      margin: 8px 12px 8px 0;
      @include card-h2();
      &-icon {
        margin: 3px;
      }
    }

    .WhatsNew-linkGroup {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: flex-end;
      list-style: none;
      padding: 0;

      @include lessThan($medium) {
        justify-content: flex-start;
      }
    }

    .WhatsNew-linkButton {
      margin: 8px 12px 8px 0;
      @include button-text('sm');
      &-inner {
        display: inline-flex;
        align-items: center;
      }
      &-icon {
        width: 1em;
        height: 1em;
        margin-right: 4px;
      }
      &-v-icon {
        color: currentColor;
        margin-right: 4px;
      }
    }
  }

  .WhatsNew-list {
    padding-left: 0;
    list-style-type: none;

    &-item {
      &-anchor {
        text-decoration: none;
        margin: 5px;
        @include font-size(14);

        @include lessThan($medium) {
          display: flex;
          flex-wrap: wrap;
        }

        &-time {
          flex: 0 0 90px;

          @include lessThan($medium) {
            flex: 0 0 100%;
          }

          color: $gray-1;
        }

        &-link {
          flex: 0 1 auto;

          @include text-link();

          @include lessThan($medium) {
            padding-left: 8px;
          }
        }

        &-ExternalLinkIcon {
          margin-left: 2px;
          color: $gray-3 !important;
        }
      }
    }
  }
}
</style>
