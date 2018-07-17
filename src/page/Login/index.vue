<style lang="less" scoped src="./index.less" ></style>

<template>
  <div class='crad'>
    <div>
      <div class='title'>
        <div class='background-img'>
          <div class='title-block'>
            <img class='img' src='../../assets/images/tou.jpg' />
          </div>
          <div class='background'>
            <img class='blue-icon' src='../../assets/images/label@2x.png' />
            <img class='gender' src='../../assets/images/man_2@2x.png' />
            <div class='pos-text'>{{submitForm.name}}</div>
          </div>
          <div class='text-top'>
            <div class='text'>
              <span>云算编号：{{submitForm.account}}</span>
              <span class='right'>电话号码：{{submitForm.tel}}</span>
            </div>
            <div class='text but'>
              <span>任职公司：{{submitForm.company_name}}</span>
              <span class='right'>入职年限：{{getYearLimit(submitForm.create_time)}}</span>
            </div>
          </div>
        </div>
      </div>
      <div class='title'>
        <div class='background-image'>
          <div class='title-block'>
            <img class='img' src='../../assets/images/tou.jpg' />
          </div>
          <div class='background'>
            <img class='blue-icon' src='../../assets/images/label@2x2.png' />
            <img class='gender' src='../../assets/images/girl_2@2x.png' />
            <div class='pos-text'>{{submitForm.name}}</div>
          </div>
          <div class='text-top'>
            <div class='text'>
              <span>云算编号：{{submitForm.account}}</span>
              <span class='right'>电话号码：{{submitForm.tel}}</span>
            </div>
            <div class='text but'>
              <span>任职公司：{{submitForm.company_name}}</span>
              <span class='right'>入职年限：{{ getYearLimit(submitForm.create_time) }}</span>
            </div>
          </div>
        </div>
      </div>
      <div class='bottom'>
        <span class='code'>
          <img class='code-img' src='../../assets/images/tou.jpg' />
        </span>
        <span class='download'>
          <div class='bottom-text'>想要了解更多经纪人信息</div>
          <div class='bottom-text'>下载云算APP！</div>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      submitForm: {
        name: "",
        account: "",
        create_time: "",
        company_name: "",
        tel: ""
      }
    };
  },

  mounted() {
    this.getShare();
  },
  methods: {
    async getShare() {
      let res = await this.api.getShare({ id: 1 });
      if (res.code == 200) {
        this.submitForm = res.data;
      }
    },
    getYearLimit(create_time_str) {
      let dateStr = create_time_str.split(" ")[0];
      let dateArr = dateStr.split("-");
      let create_time = new Date(dateArr[0] , dateArr[1] - 1 , dateArr[2]);
      let nowTime = new Date();
      let nowDate = new Date(nowTime.getFullYear() , nowTime.getMonth() , nowTime.getDate());
      //计算时间跨度
      let distance = nowDate.getTime() - create_time.getTime(); 
      let result = "";
      let year = Number.parseInt( distance / 1000 / 60 / 60 / 24 / 365 ) ; //转整
      if(year>0) {
        result += year + "年";
      }

      let month = Number.parseInt( distance / 1000 / 60 / 60 / 24 / 30 ) ; 
      if(month > 0 ) {
        let month_dist = month - year * 12;
        result += month_dist + "个月";
      }

      return result;

    }
  }
};
</script>



