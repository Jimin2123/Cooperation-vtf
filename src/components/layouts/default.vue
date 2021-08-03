<template>
  <v-app>
    <v-system-bar window lights-out height="20"></v-system-bar>
    <v-app-bar app color="white" flat>
      <v-app-bar-nav-icon class="ml-10" @click.stop="draw = !draw" v-if="!draw"/>
      <v-toolbar-title v-if="!draw">
        <v-tooltip bottom >
          <template v-slot:activator="{ on, attrs }">
            <v-btn v-bind="attrs" v-on="on" text class="pa-0">Cooperation</v-btn>
          </template>
            <span>Bottom tooltip</span>
        </v-tooltip>
      </v-toolbar-title>
      <v-spacer/>
      <v-btn icon><v-icon>mdi-magnify</v-icon></v-btn>
      <v-btn icon v-if="!user"><v-icon>mdi-account</v-icon></v-btn>
      <v-btn icon v-else>
        <v-avatar size="30px">
          <v-img src="https://avatars2.githubusercontent.com/u/67082137?s=460&u=f69e0bb8fbf80e5c67c541ae99bd4868100a5e17&v=4">
          </v-img>
        </v-avatar>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer
      v-model="draw"
      app
    >
    <v-list-item>
      <v-list-item-avatar size="40px" color="grey"></v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title>Cooperation</v-list-item-title>
          <v-list-item-subtitle>웹 사이트 버전</v-list-item-subtitle>
        </v-list-item-content>
      <v-list-item-action>
        <v-btn icon @click.stop="draw = false">
          <v-icon size="16px" light>mdi-close</v-icon>
        </v-btn>
      </v-list-item-action>
    </v-list-item>
    <v-divider />
    <!-- 유저 -->
    <v-expansion-panels v-if="user" focusable max="255px">
      <v-expansion-panel>
        <v-expansion-panel-header>
          <v-list-item>
            <v-list-item-avatar>
              <v-img
                src="https://avatars2.githubusercontent.com/u/67082137?s=460&u=f69e0bb8fbf80e5c67c541ae99bd4868100a5e17&v=4"
              ></v-img>
            </v-list-item-avatar>

            <v-list-item-content>
              <v-list-item-title>유저 이름</v-list-item-title>
              <v-list-item-subtitle>등급</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
          <template v-slot:actions>
            <v-icon color="primary">$expand</v-icon>
          </template>
        </v-expansion-panel-header>
        <v-expansion-panel-content >
          <v-list>
            <v-list-item v-for="ui in userItems" :key="ui.title" link>
              <v-list-item-icon>
                <v-icon>{{ ui.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-content>{{ ui.title }}</v-list-item-content>
            </v-list-item>
          </v-list>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <v-list>
      <v-list-group
        v-for="(item, i) in items " :key="i"
        :prepend-icon="item.icon"
        no-action
      >
        <template slot="activator" block>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </template>
          <v-list-item
            v-for="(sub,j) in item.sub" :key="j" link :to="sub.to"
            class="pl-10"
          >
          <v-list-item-icon>
            <v-icon>{{sub.icon}}</v-icon>
          </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title v-if="sub.chip">
                {{ sub.title}} | <v-chip v-if="sub.chip" label small :color="sub.color" >{{ sub.chip }}</v-chip>
              </v-list-item-title>
              <v-list-item-title v-else>{{ sub.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
      </v-list-group>
    </v-list>
    </v-navigation-drawer>
    <!-- content -->
    <v-main>
    </v-main>
    <!-- footer -->
    <v-footer absolute app color="white" class="pa-0">
      <v-card flat width="100%" light>
      <v-divider/>
        <v-subheader light>
          <v-btn text class="caption">개인정보처리방침</v-btn>|<v-btn text class="caption">이용약관</v-btn>
          <v-spacer />
          <span class="caption"> &copy; {{ new Date().getFullYear() }} Shiba</span>
        </v-subheader>
      </v-card>
    </v-footer>

  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class Default extends Vue {
  draw = false
  user = false
  userName = '정지민'
  items = [
    {
      title: '메인',
      icon: 'mdi-home',
      sub: [
        {
          title: '홈',
          icon: 'mdi-home-outline',
          to: '/'
        },
        {
          title: '전체 게시물',
          icon: 'mdi-layers-triple-outline',
          to: '/article'
        },
        {
          title: 'BEST 게시물',
          icon: 'mdi-trophy-outline',
          to: '/bestBoard'
        },
        {
          title: 'HOT 게시판',
          icon: 'mdi-fire',
          to: '/fireBoard'
        },
        {
          title: 'Commit 순위',
          icon: 'mdi-git',
          to: '/rank'
        }
      ]
    },
    {
      title: '프로젝트',
      icon: 'mdi-account-group',
      sub: [
        {
          title: 'All',
          icon: 'mdi-border-all-variant',
          to: '/project'
        },
        {
          title: '스터디',
          icon: 'mdi-book-open-page-variant',
          to: '/study'
        },
        {
          title: 'Teams',
          chip: '모집중',
          color: 'primary',
          icon: 'mdi-application-import',
          to: '/recruiting'
        },
        {
          title: 'Teams',
          chip: '진행중',
          color: 'warning',
          icon: 'mdi-application-cog',
          to: '/ongoing'
        },
        {
          title: 'Teams',
          chip: '완료',
          color: 'success',
          icon: 'mdi-application-export',
          to: '/done'
        }
      ]
    },
    {
      title: '커뮤니티',
      icon: 'mdi-comment-text-multiple',
      sub: [
        {
          title: '공지사항',
          icon: 'mdi-antenna',
          to: '/notice'
        },
        {
          title: '질문',
          icon: 'mdi-comment-question-outline',
          to: '/question'
        },
        {
          title: '일상',
          icon: 'mdi-chart-timeline',
          to: '/daily'
        },
        {
          title: '포럼',
          icon: 'mdi-forum-outline',
          to: '/forum'
        },
        {
          title: '코드 리뷰',
          icon: 'mdi-file-code-outline',
          to: 'code-review'
        },
        {
          title: '기술 서적 리뷰',
          icon: 'mdi-book-open-outline',
          to: '/teachBook-review'
        }
      ]
    },
    {
      title: "JOB'S",
      icon: 'mdi-office-building',
      sub: [
        {
          title: '구인',
          chip: '계약직',
          color: 'success',
          icon: 'mdi-account-plus-outline',
          to: '/job-type-contract'
        },
        {
          title: '구인',
          chip: '정규직',
          color: 'primary',
          icon: 'mdi-account-plus-outline',
          to: 'job-type-fulltime'
        },
        {
          title: '구직',
          icon: 'mdi-account-question-outline',
          to: '/resumes'
        },
        {
          title: '회사 평가',
          icon: 'mdi-book-information-variant',
          to: '/evaluation'
        }
      ]
    },
    {
      title: '관리 메뉴',
      icon: 'mdi-laptop-mac',
      sub: [
        {
          title: '사용자 관리',
          icon: 'mdi-account-details',
          to: '/'
        }
      ]
    }
  ]

  userItems = [
    { title: '유저 정보 확인', icon: 'mdi-account' },
    { title: '진행중인 프로젝트 확인', icon: '' },
    { title: '관심있는 프로젝트', icon: 'mdi-bookmark-check' }
  ]
}
</script>

<style scoped>
  .b {
    font-size: 15px;
    color: grey;
  }
</style>
