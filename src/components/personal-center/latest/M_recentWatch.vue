<template>
  <div>
    <M-Header pageTitle="最近观看">
    </M-Header>
    <div class="container">
      <div v-for="(record,index) in records" :key="index">
        <div class="date">
          <i class="icon"></i>
          <span>{{record.data}}</span>
        </div>
        <ul>
          <li>
            <div class="course" v-for="(message,index) in (record.dataList)" :key="index">
              <div class="course-logo" :style="{backgroundImage: 'url(' + message.VideoImg+ ')'}">
                <img src="/static/mob-img/play.png"/>
              </div>
              <div class="course-intro">
                <p class="title">{{message.Title}}</p>
                <p class="time"><span>{{message.NowTimeStr}}</span>/<span>{{message.TotalTimeStr}}</span></p>
                <mt-progress :value="message.Progress" :bar-height="8"></mt-progress>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
  import {getRecentWatch} from '@/API';

  export default {

    name: 'M-recentWatch',
    components: {
      'M-Header': resolve => require(['@/components/common/Header'], resolve)
    },
    data() {
      return {
        records: [
          {
            date: '今天',
            messages: [
              {
                coursesImg: '/static/mob-img/recentCourse.jpg',
                title: '[宏观经济学分析] 江苏工商本<精讲1>-录音.mp4',
                nowtime: '00:00:00',
                totaltime: '02:56:36',
                progress: 80
              },
              {
                coursesImg: '/static/mob-img/recentCourse.jpg',
                title: '[宏观经济学分析] 江苏工商本<精讲2>-录音.mp4',
                nowtime: '00:00:00',
                totaltime: '02:56:36',
                progress: 20
              }
            ]
          },
          {
            date: '3天前',
            messages: [
              {
                coursesImg: '/static/mob-img/recentCourse.jpg',
                title: '[宏观经济学分析] 江苏工商本<精讲18>-录音.mp4',
                nowtime: '00:00:00',
                totaltime: '02:56:36',
                progress: 60
              },
              {
                coursesImg: '/static/mob-img/recentCourse.jpg',
                title: '[宏观经济学分析] 江苏工商本<精讲22>-录音.mp4',
                nowtime: '00:00:00',
                totaltime: '02:56:36',
                progress: 10
              }
            ]
          }
        ]
      };
    },
    created() {
      getRecentWatch().then(data => {
        console.log(JSON.parse(data[0].msg));
        this.records = JSON.parse(data[0].msg);
      });
    },
    mounted() {

    },
    methods: {}
  };
</script>
<style>
  .mt-progress {
    height: 14px;
    line-height: 28px;
  }
</style>
<style scoped>
  .date {
    margin: 0.9375rem
  }

  .date sapn {
    font-size: 0.9375rem;
  }

  .course {
    /*margin: 0.5rem 0.9375rem 0  0.9375rem ;*/
    padding-bottom: 0.5rem;
    margin: 0.5rem 0.5rem 0 0.5rem;

    border-bottom: 1px solid #d8d8d8;
    overflow: hidden;
  }

  .course-logo {
    width: 4.6875rem;
    height: 4.6875rem;
    float: left;
    /*border:1px solid red;*/
    /*background-image: url('../../../static/img/lesson.png');*/
    background-repeat: no-repeat;
    background-size: cover;
    position: relative;
  }

  .course-logo img {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    height: 1.40625rem;
    width: 1.40625rem;
  }

  .course-intro {
    margin: auto 0.625rem;
    width: 16.3125rem;
    float: left;
  }

  .course-intro p {
    margin-bottom: 0.15625rem;
  }

  .title {
    font-size: 0.875rem;
    font-weight: bold;
  }

  .time {
    font-size: 0.75rem;
    font-weight: lighter;
    color: #999999;
    margin: 1.09375rem 0 0.46875rem 0;

  }

  .icon {
    width: 0.46875rem;
    height: 0.46875rem;
    background-image: url('/static/mob-img/icon.jpg');
    background-repeat: no-repeat;
    background-size: 100% 100%;
    display: inline-block;
  }
</style>
