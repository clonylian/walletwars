<template>
  <div :class="showno == 0 ? 'ymain' : 'ydisnone ymian'">
    <div class="ybuts">
      <div class="ybutbg"></div>
      <h2>LOGIN</h2>
      <button @click="twitterlog()">
        <img src="../assets/twitter-x.svg" alt="" />
        <span>Continue with X</span>
      </button>
      <div class="dkeor">
        <span class="dkehs"></span>
        <span>Or</span>
        <span class="dkehs"></span>
      </div>
      <div class="ythricon">
        <div class="ygoogle" ref="googlesignin"></div>
        <div class="ytwitter" @click="render()">
          <img src="../assets/a5c8d5f5e044e626e6238a962c5cbd8.png" alt="" />
        </div>
      </div>
      <div class="dkeendtxt">
        By continuing, you agree to accept our Term &amp;<br />Conditions and
        Privacy Policy
      </div>
      <img
        @click="ongb()"
        class="gb"
        src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAHAAAABwCAYAAADG4PRLAAAACXBIWXMAABYlAAAWJQFJUiTwAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAhkSURBVHgB7Z2PcdNIFMZfEg+YGWaOVICogHSAqIBQAbkKCBUQKiBXAVABSQXxVYCpIKKCmBkwhsTxvS+sDnu1ku39v87+ZjSO5dha7ae3+/bt04ook8lkMplMJpPJZDKZTCaTyWQ2ny1KmNls9mAymezx616v13uI97wV/FEh/+/W1taIPxvxn6Pt7e3q6urqC+8b9vv9IT6jRElKQAj069evkiv8yfX19T4phNIBQvILttM7d+4MUhI0egFrK+NKfc1v93h7QO454eOe3rt37z1FTrQCCmt7ya+H5Ec0FRVfOAO29jcsZkUREp2AFoSrxOtIbDWF+D2ti4GFfB+jkNEIqCHcjXVMp9PP/J2KHZPhqpX748ePgl8KOD/8vSf0u2kuVvkuH/OIhfwQi5BRCPjz5899rsx3tFw4NGenXIkntitQiAoH6QVel/x7xeV9E0MfGVRAWB2L95G6Kwzu/z/s7h/78g4hJloCts5n1GGZsTarXuBKKtm7POdt1rKdj8fjQ4hMAeFyHiwrJ86FbhNsda87KuSCK+QotHAyKBPK1lZunBPdBvhk33aIdyb6oihB2Xh731H+t7SpiAH5WZvV8XZIiYCydljjR5+thxcnRgwRzuC2Kz6GR/c0NUcA1shOzBmp465DDsk9TTnGukCH5Z3F1tetA0TsOjfaBNr6PPQltCG09Yvs2LyjlGnzNjdJvJoOEdP0ThFduS3i1bSJmNw4UfQN5yoPjTYcVZ/IF/OFq+HRNjmAvS+0/YW0u7p79+7ftOGwUM/pz4zIDXDURJ1Yx7qACD1RM7aJeObmuNUd7O7u3pwrLU5lgTL6sW5b0ylEvVWIGGqjKY162AS3eeNcaQPQ5ycTbhPWp4rUF6QBR25exCA+yoCykAYXFxcPVCG3KOO9KuvTbTpRYTFY8Pw56Yoo4qZxt0pt1kcazIsX8oRVF6SBiOeurNCKF8oz141oA1IOSAOe4T5U/NaBTxFxLByTmuXQ8iKn0+kreR975HF4pDatD4h+41Oo2KLK8sSxP5l4kLIV2vJIbVhgKe/QtT6AcRRfFBhHDRW/69QS2yzPxvQQ/+4H6T3ygQ7IEGMBRRaXzIAMCCGiS/EAW90xNQf3zygkquZzPB6fkCV8Naeumk0ZVZzU9PdNLbCUdyBnkyzhwxJdW948cjMqjn9ABhgJKPImF+j3+9YEBC5F9CkeYItr1A173SWFQhFlcJZGYLs59dVsysjNKLxRMkDbAnlQq7rV6zM5wqYl+ra8edjiFupI3JT6kDTRFvDy8rKQ9/GAdUAOsSFiSPHq48j72BKfkibaAnL/10gRxF1C5BgTEUOLB3Z2doaK3QVpYiLgY3nf/fv3h+QBHRFjEA98//69kvdxXfpvQuWO3vds+zoixiIeQLmpmXJRkCY90qegxUJU5BlUBnunyOqG97snlQci/v+3/N3A2dPyMQvSxGQcKHugQfJdlllihOKBheNyObSHLTYFDEaXiDIx3LcgH9tk3GktK40LVVFAVhExBvEAjwW/kiWc5IWGAiKqxllzJL0qkwprAvIgfpcC0+Zt1vie2W+Dhw1/kSVMBFy4km0WSodl4tXEIKLNIZg1ASmgU9M1zqMAM/vrIhbh0yJ5AZcN0kOlZyyhkN5XpIlJJEaeeSjIM6tEWELm2HRQzL8x8UpNBBwp9mnH9NZlnfBYTCKKabgFlnjOnWgLaHtaZB10YpuxiKiahmML9C8gKTLPuOL2yDEmgekYROTyldQ8dkWaaAsolgWRK+sxOcTGrEJoEeVpOJTZZBrOdCA/lAqz5yqfxOaUUCgRkddDUiYfH09bPGAkIJZ+pMXC3CyPTJZxMZ8XQkQua6nYfUoGGAmoygHlJkLrDp42XE7G+hax1+s9UxznhEKiSpOz1Yz6Sv3zkQHecrPnJzLEOJjNFfmv9N7KTRs+0yB8WGK/398nKVqFhWwpNOLKmtlM8A2VdOvSEl3e5GkMlk1WFK4kDUKJV+NCRLE6sZOm2cp8IHujjaZAPKhD57e+KH7L20x6V3OqKtsqqBb5wVrbFBMT9RJT+6SBWN7Yq+XJyJaIMpEGLevFxLf0iqqZQLuvW/mosFDi1dQi6oonxsXx9n0yE8sL24QUzwYTxVqptq3P6pLLYhlijG1kdxnJtwO6RaBFEksyL8B18cjm8tJWs9JQMNXYBp14tM2GA8SF3LC02e+nvVRkESeLnosIgxwTHfBg1st8YWhE3y2ff8Xn/4gs4yQvlAuPNTNll7+cbPJzFQQ4R4V49RKU6TBRrBEmOnGt8WEKdDyR5pBSZDweH98WETvEO6aUmbQ8V2GTRGwTD30hpU5XbHET+sRJ+7Ogzn2MY708emfZY2o4Lvg80UfvYKhQKj729jghL3cnifEhvLBK/gweG8RN6dkKc4P0Uv4MF+QswWdBrYRoTs9ampyZcMGjDZ+J2Gbn4/NSD/+tRJt3WvcdMa5yL55Ec95R7rS9zXWZdD+DrxaypMCIWZauViPosw+9ODFtdDk3c3h/YjSaQbQCYjG/su3/YnDAggpYg/m2FWbwRyKN8ZRn5we2Z+frnFakRfLfjQQkuSwI2rNwRxSYKAQEYrbiqGUFYBUDZMRxhQ8vLy+rddPTcTwsF8bHe8JWhNilavE+FSd83FexeJnRCFijIeQ8ldgaq2ZgNSSsxyK8xILWZyCa8gFFRHQC1hgKaZMT0VwOKEKiFbBGCImB80tqzjG64qZ55vm7Yx+ZcCZEL+A8EBMOhvAOV+2zVgEiwaM8haOUUhQlKQFlvn37Biek2NnZKfktbu+u+7dC8e+jehPhrq+4tWs6nQ59LZOZyWQymUwmk8lkMplMJpPJZDKZTCaTyWQy6/AfDu/75DfiRbIAAAAASUVORK5CYII="
        alt=""
      />
    </div>
  </div>
  <div class="ycont">
    <video
      height="100%"
      autoplay
      muted
      loop
      src="../assets/screen_recorder.webm"
    ></video>
    <div class="ycontbut">
      <a href="#">
        <img src="../assets/x.png" alt="" />
      </a>
      <a href="#">
        <img src="../assets/discord.png" alt="" />
      </a>
    </div>
  </div>
</template>
<script setup>
import hello from "hellojs/dist/hello.all";
import { onMounted, ref } from "vue";
let googlegloin = ref(null);
let googlesignin = ref(null);
let showno = ref(0);
//登录twitter
let twitterlog = () => {
  hello.init(
    {
      twitter: "推特对应的key",
    },
    {
      redirect_uri: "配置的本地地址或者上线地址",
    }
  );
  hello("twitter")
    .login()
    .then(
      function (res) {
        console.log(res, "登录成功");
      },
      function (err) {
        console.log("err", err);
      }
    );
  hello.on("auth.login", (result) => {
    hello(result.network)
      .api("/me")
      .then(
        function (p) {
          console.log(result, "result");
        },
        function (err) {
          console.log("err", err);
        }
      );
  });
};
onMounted(() => {
  //登录google
  window.onload = function () {
    google.accounts.id.initialize({
      client_id:
        "281527463753-vebj64f9ejc2rqi4v4650j9one2ku7bb.apps.googleusercontent.com",
      callback: handleCredentialResponse,
    });
    // google.accounts.id.prompt();
    google.accounts.id.renderButton(googlesignin.value, {
      theme: "outline",
      size: "large",
      type: "icon",
      shape: "pill",
      click_listener: onClickHandler,
    });
  };
});
let handleCredentialResponse = async (response) => {
  let code = response.credential;
  console.log(code);
};
let onClickHandler = (user) => {
  console.log(user, "Sign in");
};
//web3modal
let render = () => {
  main();
  ongb();
};
//关闭弹窗
let ongb = () => {
  showno.value = 1;
};
let tiaoz = () => {
  window.location.href = "#";
};
</script>
<style scoped>
.ydisnone {
  display: none;
}
.ymain {
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.25);
  width: 100vw;
  height: 100vh;
  position: fixed;
  z-index: 20;
}
.ybuts {
  width: 25.6rem;
  border-radius: 1rem;
  background: rgba(0, 0, 0, 0.75);
  padding: 2rem;
  box-sizing: border-box;
  position: relative;
}
.ybutbg {
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  height: 0.75rem;
  background: linear-gradient(180deg, #7149e2 0%, #8296eb 100%);
  border-top-right-radius: 1rem;
  border-top-left-radius: 1rem;
}
.ybuts > button {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 60%;
  padding: 0.5rem 0.75rem;
  box-sizing: border-box;
  border: 1px solid #dadce0;
  font-weight: 700;
  color: rgb(15 20 25);
  margin: 1rem auto;
  background: #fff;
  border-radius: 1.5rem;
  column-gap: 0.5rem;
  cursor: pointer;
  font-size: 1rem;
}
.ybuts > h2 {
  font-size: 2rem;
  line-height: 2rem;
  color: #fff;
  text-align: center;
}
.ybuts > button:hover {
  background: rgb(230, 230, 230);
}
.ybuts > button > svg {
  width: 1.5rem;
  height: 1.5rem;
}
.ybuts > button > img {
  width: 1.5rem;
  height: 1.5rem;
}
.dkeor {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 1.375rem;
  margin: 1rem auto 0.5rem;
  padding: 0.5rem 0.75rem;
  box-sizing: border-box;
}
.dkehs {
  width: 39%;
  height: 1px;
  background: rgba(255, 255, 255, 0.35);
  font-weight: 700;
}
.dkeor > span {
  font-style: normal;
  font-weight: 400;
  font-size: 1rem;
  line-height: 1.125rem;
  color: #f8f8f8;
  padding: 0 1rem;
}
.ythricon {
  display: flex;
  justify-content: center;
  align-items: center;
  column-gap: 1.5rem;
  padding: 0 0 1rem;
}
.ytwitter {
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 50%;
  background: #fff;
  cursor: pointer;
  position: relative;
  border: 1px solid #fff;
  transition: border-color 0.218s;
  box-sizing: border-box;
  overflow: hidden;
}
.ytwitter:hover {
  border-color: #d2e3fc;
}
.ytwitter > img {
  width: 85%;
  position: absolute;
  left: 0.225rem;
  top: 0;
}
.dkeendtxt {
  width: 100%;
  padding: 0 1.25rem;
  font-style: normal;
  font-weight: 400;
  font-size: 0.75rem;
  line-height: 1rem;
  text-align: center;
  color: #9d9d9d;
  box-sizing: border-box;
}
.gb {
  width: 2rem;
  cursor: pointer;
  position: absolute;
  left: 50%;
  bottom: -3rem;
  transform: translate(-50%);
}
.ycont {
  width: 100%;
  height: 100vh;
  position: relative;
  overflow: hidden;
}
.ycont > video {
  width: 110%;
  position: absolute;
  z-index: 1;
  left: 0;
  transform: translate(-5%);
}
.ycontbut {
  width: 100%;
  position: absolute;
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 20%;
  column-gap: 1.25rem;
}
.ycontbut > a {
  width: 2rem;
}
.ycontbut > a > img {
  width: 100%;
}

@media (max-width: 1250px) {
  .ycont > video {
    width: 384%;
    transform: translate(-37%);
  }
  .cornered-button {
    font-size: 1.25rem;
  }
}
</style>
