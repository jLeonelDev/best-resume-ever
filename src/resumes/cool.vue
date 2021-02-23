<template>
  <div class="resume">
    <div class="banner">
      <div class="banner__fullname">{{ person.name.first }} {{ person.name.middle }} {{ person.name.last }}</div>
      <div class="banner__position">{{ person.position }}</div>
      <div v-if="person.birth" class="banner__location">{{ lang.born }} {{person.birth.year}} {{ lang.bornIn }} {{person.birth.location}}</div>
    </div>

    <div class="content">
      <div class="content__left">
        <div class="section">
          <div class="section-headline">
            {{ lang.about }}
          </div>

          <div class="section-content section-content--plain">
            {{ person.about }}
            <br/>
            <br/>
            {{ person.knowledge }}
          </div>
        </div>

        <div
          v-if="person.skills"
          class="section">
          <div class="section-headline">
            {{ lang.skills }}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(skill, index) in person.skills"
              class="grid-item"
              :key="index"
              :href="skill.url">
              <span class="squarred-grid-item">
                {{ skill.name }}
              </span>
            </a>
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            {{ lang.contact }}
          </div>

          <div class="section-content section-content--plain">
            <div class="section-link">
              <i class="section-link__icon material-icons">business</i>{{ person.contact.street }}
            </div>

            <a
              class="section-link"
              :href="contactLinks.email">
              <i class="section-link__icon material-icons">mail</i>{{ person.contact.email }}
            </a>

            <div class="section-link">
              <i class="section-link__icon material-icons">phone</i>{{ person.contact.phone }}
            </div>

            <a
              v-if="person.contact.website"
              class="section-link"
              :href="person.contact.website">
              <i class="section-link__icon fa fa-globe"></i>{{ person.contact.website }}
            </a>

            <a
              v-if="person.contact.linkedin"
              class="section-link"
              :href="contactLinks.linkedin">
              <i class="section-link__icon fa fa-linkedin"></i>{{ person.contact.linkedin }}
            </a>

            <a
              v-if="person.contact.github"
              class="section-link"
              :href="contactLinks.github">
              <i class="section-link__icon fa fa-github"></i>{{ person.contact.github }}
            </a>

            <a
              v-if="person.contact.medium"
              class="section-link"
              :href="contactLinks.medium">
              <i class="section-link__icon fa fa-medium"></i>{{ person.contact.medium }}
            </a>
          </div>
        </div>
      </div>

      <div class="content__right">
        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">work</i>{{ lang.experience }}
          </div>

          <div class="section-content">
            <a
              v-for="(experience, index) in person.experience"
              :key="index"
              class="section-content__item"
              :href="experience.website">

              <span class="section-content__header">{{ experience.position }}</span>
              <span class="section-content__subheader">
                {{ experience.company }}
                <span class="section-content__plain">{{ experience.location }}</span>
              </span>

              <div class="section-content__plain">{{ experience.timeperiod }}</div>
              <template v-for="(description, index) in experience.description" >
                <span :key="index" class="section-content__text--light--inline">&bull; {{ description }}</span>
              </template>
            </a>
          </div>
        </div>

        <div class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">school</i>{{ lang.education }}
          </div>

          <div class="section-content">
            <a
              v-for="(education, index) in person.education"
              class="section-content__item"
              :key="index"
              :href="education.website">

              <span class="section-content__header"> {{ education.school }} </span>
              <span class="section-content__subheader">{{ education.degree }}</span>
              <span class="section-content__text"> {{ education.timeperiod }} </span>
              <span class="section-content__text--light"> {{ education.description }} </span>
            </a>
          </div>
        </div>

        <div
          v-if="person.projects"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon material-icons">code</i>{{ lang.projects }}
          </div>

          <div class="section-content-grid">
            <a v-for="(project, index) in person.projects" :key="index"
              class="section-content__item-grid"
              :href="project.url">
              <span class="section-content__header"> {{ project.name }} </span>
              <span class="section-content__subheader">{{ project.platform }}</span>
              <span class="section-content__text"> {{ project.description }} </span>
            </a>
          </div>
        </div>

        <div
          v-if="person.contributions"
          class="section">
          <div class="section-headline">
            <i class="section-headline__icon fa fa-heart"></i>{{lang.contributions}}
          </div>

          <div class="section-content-grid">
            <a
              v-for="(contribution, index) in person.contributions"
              class="section-content__item-grid"
              :key="index"
              :href="contribution.url">
              <span class="section-content__header"> {{ contribution.name }} </span>
              <span class="section-content__text"> {{ contribution.description }} </span>
              <span class="section-content__text--light" style="word-break: break-all;">
                {{ contribution.url }}
              </span>
            </a>
          </div>
        </div>
      </div>
    </div>

    <img class="picture"/>
  </div>
</template>

<script>
import Vue from 'vue';
import { getVueOptions } from './options';

const name = 'cool';

export default Vue.component(name, getVueOptions(name));
</script>

<style lang="less" scoped>
@accent-color: #4A154B;
@banner-color: #aa8121;
@banner-tiles-color: white;
@content-color: white;
@tiles-color: #ECB22E;
@banner-height: 70px;
@picture-size: 150px;
@picture-offset: 50px;
@base-padding: 20px;
@left-column-width: 185px;

a {
  color: inherit;
  cursor: pointer;
  text-decoration-line: none;

  &:visited {
    color: inherit;
  }
}

.resume {
  position: relative;
  font-family: -apple-system, BlinkMacSystemFont !important;
  font-size: 1em;
  background-color: rgb(236, 236, 236);
}

.picture {
  position: absolute;
  top: @banner-height - @picture-offset;
  left: @left-column-width + @base-padding * 22 - @picture-size / 2;
  height: @picture-size;
  width: @picture-size;
  border-radius: 50%;
  border: 3px solid @banner-color;
  content: url('../../resume/id.jpg');
  z-index: 2;
}

.banner {
  width: calc(100% - @base-padding * 2);
  height: @banner-height;
  padding: @base-padding;
  background-color: @banner-color;
  /*
    background-image: url('../../resume/banner.png');
    background-repeat: no-repeat;
    background-size: cover;
  */
  color: @banner-tiles-color;

  &__fullname {
    font-size: 35px;
  }

  &__position {
    font-size: 18px;
  }

  &__location {
    font-size: 10px;
  }
}

.content {
  display: flex;
  width: 100%;
  height: 100%;

  &__left,
  &__right {
    height: 100%;
    padding: @base-padding;
  }

  &__left {
    width: @left-column-width;
    color: @content-color;
    background-color: @accent-color;

    .section-headline {
      color: @tiles-color;
    }
  }

  &__right {
    flex: 1;
  }
}

.section {
  margin: 0px, 0;
}

.section-link,
.section-headline {
  display: flex !important;
  align-items: center;
  color: @accent-color;
  display: inline-block;
  font-size: 1.2em;
  margin: 8px 0;

  &__icon {
    margin-right: 4px;
    font-size: 1.2em;
  }
}

.section-link {
  font-size: 1.1em;
  color: @content-color !important;

  &__icon {
    color: @tiles-color;
  }
}

.section-content {
  margin-top: 0px;
  padding-left: 0px;
  font-size: 12px;

  &__item {
    display: block;
    margin-bottom: 5px;
  }

  &__header {
    color: @banner-color;
    display: block;
    font-size: 1.06em;
    font-weight: 700;
  }

  &__subheader {
    color: @accent-color;
    font-size: 1.06em;
    display: block;
    font-weight: 600;
  }

  &__plain,
  &__text {
    display: block;
    font-size: 12px;

    &--light {
      font-size: 12px;

      &--inline {
        display: inline-block;
      }
    }
  }

  &__plain {
    display: block;
    font-weight: 200;
  }

  &__item-grid {
    flex: 1 1 0;
    margin-bottom: 5px;
    padding-right: 5px;
  }

  &--plain {
    padding: 0;
  }
}

.section-content-grid {
  display: flex;
  flex-wrap: wrap;
  margin-top: 5px;
  margin-bottom: 5px;
  font-size: 12px;
}

.grid-item {
  padding-right: 5px;
}

.squarred-grid-item {
  display: block;
  border: 1px solid @content-color;
  color: @content-color;
  margin-top: 5px;
  padding: 5px;
}
</style>
