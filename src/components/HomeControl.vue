<template>
  <div>
    <div :class="theme">
      <div class="InnerborderBox">
        <div class="Innerborder">
          <div class="Horsebox">
            <div class="pen">
              <svg  xmlns="http://www.w3.org/2000/svg"  width="100%" height="100%" viewBox="0 0 30 30"  fill="none"  stroke="white"  stroke-width="2"  stroke-linecap="round"  stroke-linejoin="round"  class="icon icon-tabler icons-tabler-outline icon-tabler-hierarchy">
                <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                <path d="M12 5m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
                <path d="M5 19m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
                <path d="M19 19m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
                <path d="M6.5 17.5l5.5 -4.5l5.5 4.5" />
                <path d="M12 7l0 6" />
              </svg>
            </div>
            <h1 class="move0">{{ fullDate }}</h1>
            <h1 class="move">{{ hourseName }}</h1>
            <h1 class="move1">{{ hourseName1 }}</h1>
            <h1 class="move2">{{ hourseName2 }}</h1>
            <h1 class="move3">{{ hourseName3 }}</h1>
            <h1 class="move4">{{ hourseName4 }}</h1>
            <div class="container">
              <div class="circle">
                <img class="robot" alt="Image" :src="robotImage">
              </div>
              <div class="NameBox">
                <p>Hi, Jack Cooper</p>
              </div>
              <div class="ChevronDowBox">
                <img style="height: 24px; width: 24px; align-items: center; margin-left: auto; margin-right: 1rem; cursor: pointer;" alt="chevron-down" :src="ChevronDow">
              </div>
            </div>
          </div>
        </div>
        <div class="currentTimebox">
          <h2 class="current-time-heading">{{ currentTime }}</h2>
        </div>
        <div class="InnerborderBox2">
          <div class="weather-box">
            <button class="Weatherbutton" @click="chooseRandomWeather" :disabled="isButtonDisabled"></button>
            <div class="weather-info-box">
              <div class="weather-info">
                <img :src="weatherImage" v-if="showWeather">
              </div>
              <div class="temperaturetext1-box">
                <p class="temperaturetext1">{{ weather.temperature }}°</p>
              </div>
            </div>
            <div class="temperature-info">
              <p class="temperaturetext">{{ weather.condition }}</p>
            </div>
          </div>
          <div class="musicbox">
            <div class="music-control-box mt-4">
                <h3>Now Playing</h3>
                <img :src="cdMusicImage">
                <div class="music-info" :class="{ playing: isPlaying }">
                    <p class="track-title">{{ currentTrack }}</p>
                    <div class="wave">
                      <!-- <span v-for="i in 5" :key="i"></span> -->
                        <span></span>
                        <span></span>
                        <span></span>
                        <span></span>
                        <span></span>
                    </div>
                </div>
                <div class="music-controls">
                    <button @click="prevTrack">⏮</button>
                    <button @click="rewind">⏪</button>
                    <button @click="togglePlay">{{ isPlaying ? '⏸' : '▶️' }}</button>
                    <button @click="forward">⏩</button>
                    <button @click="nextTrack">⏭</button>
                </div>
                <div class="volume-slider">
                    <button class="volume-toggle-button" @click="toggleMute">
                        <img :src="isMuted ? muteIcon : volumeIcon" alt="Volume Icon">
                    </button>
                    <input type="range" min="0" max="100" v-model="volume">
                </div>
            </div>
          </div>
        </div>
        <div class="AirConditionerBox">
          <div class="AirConditionerinBox">
            <div class="air-header">
              <img class="WifiIcon" :src="WifiIcon">
              <span class="time-date">AirConditioner</span>
              <img class="setingIcon" :src="setingIcon">
            </div>
            <div class="AirConditionerIconBox">
              <img class="AirConditionerIcon" :src="AirConditionerIcon" alt="AirConditioner Icon">
            </div>
            <div class="circle-container">
              <div class="pluscontrol">
                  <button class="plusIcon" @click="increaseTemperature">
                    <img :src="plusIcon" alt="Plus Icon" />
                  </button>
              </div>
              <div class="circle-screen">
                <div class="rotating-needle" :class="{ paused: !isNeedleAnimating }">
                  <svg class="needle-svg" viewBox="0 0 100 100">
                    <path d="M81.82,18.18 A45,45 0 0,1 81.82,81.82" stroke="#39FF14" stroke-width="5" fill="none" stroke-linecap="round"/>
                  </svg>
                </div>
                <div class="screen-text">
                  <span class="temperature">{{ sliderValue }}°</span>
                  <div class="power-container">
                    <button class="powerIcon" @click="PowerTemperature">
                      <img :src="powerIcon" alt="power Icon" />
                    </button>
                  </div>
                  <span class="cooling-to" style="color:#00C8FF;">COOLING TO</span>
                </div>
              </div>
              <div class="Subtractioncontrol">
                <button class="SubtractionIcon" @click="decreaseTemperature">
                  <img :src="SubtractionIcon" alt="Minus Icon" />
                </button>
              </div>
            </div>
            <div class="controlBox">
              <div class=" timebox">
                <div class="Timerinbox">
                  <img :src="TimerIcon" alt="Timer Icon" />
                  <p>Timer</p>
                </div>
                <span></span>
                <div class="Timerinbox2">
                  <p style="font-size: 25px; color: #fff;">1.5</p>
                  <p style="color: rgba(0, 0, 0, 0.6);">Hours</p>
                </div>  
              </div>
              <div class="Sleep">
                <img :src="leaftIcon" alt="left Icon" />
                <p>Power saving</p>
              </div>
              <div class="mon">
                <img :src="moonIcon" alt="moon Icon" />
                <p>Sleep</p>
              </div>
            </div>
            <div class="AirVolumeControlBox">
              <div class="AirVolume">
                <div class="AirVolumeBox">
                  <img :src="AirIcon" alt="Air Icon" />
                  <p>Air Volume</p>
                </div>
                <span></span>

                <div class="fan-speed" :class="{'active': selectedSpeed === 'high'}" @click="setSpeed('high')">
                  <p>High</p>
                </div>
                <span></span>
                <div class="fan-speed" :class="{'active': selectedSpeed === 'medium'}" @click="setSpeed('medium')">
                  <p>Medium</p>
                </div>
                <span></span>

                <div class="fan-speed" :class="{'active': selectedSpeed === 'low'}" @click="setSpeed('low')">
                  <p>Low</p>
                </div>
                <span></span>
                <div class="cycleIcon" :class="{'active': selectedSpeed === 'cycle'}" @click="setSpeed('cycle')">
                  <!-- <div class="cycleIcon"> -->
                  <img :src="cycleIcon" alt="cycle Icon" />
                  <p>Cycle</p>
                  <!-- </div> -->
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="EnergyBox">
          <div class="EnergyCharBox">
            <Line :data="chartData" :options="chartOptions" :width="800" :height="200"/>
          </div>
        </div>
        <div class="otherBox">

          <div class="MixOtherBox">     
            <div class="CCTV">
              <img :src="CCTVIcon" alt="CCTV Icon">
              <div class="ButtoncheckBox">
                <span>CCTV</span>
                <label class="switch">
                  <input type="checkbox" v-model="CCTVSwitchOn" />
                  <span class="slider"></span>
                </label>
              </div>
            </div>
          </div>
          <div class="MixOtherBox">
            <div class="LightBulb">
              <img :src="LightBulbIcon" alt="LightBulb Icon">
              <div class="ButtoncheckBox">
                <span>Smart Light Bulb</span>
                <label class="switch">
                  <input type="checkbox" v-model="LightbulbSwitchOn" />
                  <span class="slider"></span>
                </label>
              </div>
            </div>
          </div>
        </div>
        <div class="otherBox1">
          <div class="MixOtherBox">
            <div class="fan">
              <img :src="fanIcon" alt="fan Icon">
              <div class="ButtoncheckBox">
                <span>Smart fan</span>
                <label class="switch">
                  <input type="checkbox" v-model="fanSwitchOn" />
                  <span class="slider"></span>
                </label>
              </div>
            </div>
          </div>
          <div class="MixOtherBox">
            <div class="Extensioncord">
              <img :src="ExtensioncordIcon" alt="Extensioncord Icon">
              <div class="ButtoncheckBox">
                <span>Extension cord</span>
                <label class="switch">
                  <input type="checkbox" v-model="ExtensioncordSwitchOn" />
                  <span class="slider"></span>
                </label>
              </div>
            </div>
          </div>
        </div>
        <div class="homeColorBox">
          <button class="homeColorSwitch" @click="homeColorSwitch">
            <img :src="homeIcon" alt="home Icon" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
  
<script>
  import { onMounted, ref ,computed} from 'vue'
  import { Line } from 'vue-chartjs'; // 正確導入 Line 組件
  import { Chart as ChartJS, Title, Tooltip, Legend, LineElement, CategoryScale, LinearScale ,PointElement,Filler } from 'chart.js';
  
  // import VueRoundSlider from 'vue-round-slider'
  import robotImage from '../assets/images/robot.png'
  import cdMusicImage from '../assets/images/CDMUSIC.png'
  import muteIcon from '../assets/images/mute.png'
  import volumeIcon from '../assets/images/volume.png'
  import ChevronDow from '../assets/images/chevron-down.png'
  import WifiIcon from '../assets/images/icons-wifi.png'
  import plusIcon from '../assets/images/add.png'
  import SubtractionIcon from '../assets/images/minus.png'
  import setingIcon from '../assets/images/Airsetting.png'
  import powerIcon from '../assets/images/power.png'
  import AirConditionerOpen from '../assets/images/AirConditionerOpen.png'
  import AirConditionerClose from '../assets/images/AirConditionerClose.png'
  import TimerIcon from '../assets/images/timer.png'
  import leaftIcon from '../assets/images/leaf.png'
  import moonIcon from '../assets/images/moon.png'
  import AirIcon from '../assets/images/air.png'
  import cycleIcon from '../assets/images/cycle.png'
  import CCTVIcon from '../assets/images/camera.png'
  import LightBulbIcon from '../assets/images/Lightbulb.png'
  import fanIcon from '../assets/images/fan.png'
  import ExtensioncordIcon from '../assets/images/Extensioncord.png'
  import homeBlackIcon from '../assets/images/white-home.png'
  import homewhiteIcon from '../assets/images/Black-home.png'


  //chart 
  // Chart.js 註冊組件
  ChartJS.register(Title, Tooltip, Legend, LineElement, CategoryScale, LinearScale, PointElement,Filler );
  
  
  export default {
    components: {
      Line, // 在這裡註冊 Line 組件
    },
    setup() {
      const selectedSpeed= ref('medium')
      const sliderValue = ref(28)
      const fullDate = ref('') // 日期回傳
      const currentTime = ref('') // 時間回傳
      const isPlaying = ref(false) //音樂控制 
      const isMuted = ref(false) //音樂控制 
      const volume = ref(50) //音樂控制 
      const isNeedleAnimating = ref(true)  //控制冷氣特效 
      const isAirConditionerOn = ref(true) // 新增一個狀態來記錄冷氣是否開啟
      const CCTVSwitchOn = ref(false) //CCTV
      const LightbulbSwitchOn = ref(false) //Lightbulb
      const fanSwitchOn = ref(false) //fan
      const ExtensioncordSwitchOn = ref(false) //Extensioncord
      const isHomeIconBlack = ref(true) //set HomeIconBlack

      // Chart.js 數據
      const randomNumbers = ref([]);
      const generateRandomNumbers = () => {
        randomNumbers.value = Array.from({ length: 7 }, () => Math.floor(Math.random() * 100) + 1);
      };
      generateRandomNumbers();
      const chartData = ref({
        labels: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
        datasets: [
          {
            label: 'Energy(KW)',
            data: randomNumbers,
            fill: true,
            borderColor: '#FF8C00',
            tension: 0.4,
            pointRadius: 6,
            pointBackgroundColor: '#FF8C00', // 點內部橘色
            pointBorderColor: '#ffffff',     // 點外圍白色
            pointBorderWidth: 2,             // 點邊框寬度
            backgroundColor: (context) => {
              // Chart.js 會將 context 傳進來
              const chart = context.chart;
              const { ctx, chartArea } = chart;
              if (!chartArea) {
                // 在圖表尚未計算好寬高前，chartArea 可能為 undefined
                return null;
              }
              const gradient = ctx.createLinearGradient(
                0, chartArea.top,
                0, chartArea.bottom
              );
              gradient.addColorStop(0, 'rgba(255, 140, 0, 0.8)'); // 橘色(頂部)
              gradient.addColorStop(1, 'rgba(255, 140, 0, 0)');   // 透明(底部)
              return gradient;
            },
          },
        ],
      });
      const chartOptions = ref({
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend:{
            // display: true,
            // text: 'Energy(KW)',
            labels: {
              boxWidth: 0,
              boxHeight: 0,
              font: {size: 18,},
              color: '#ffffff',
              },
            },
          },
        scales:{
          y:{
            grid:{
              color:'#333'
            },
          },
        },
      });

      // 音樂的歌名
      const trackList = [
        { title: "Song A - Artist A" },
        { title: "Song B - Artist B" },
        { title: "Song C - Artist C" },
      ]
      const currentTrackIndex = ref(0)
      const currentTrack = computed(() => trackList[currentTrackIndex.value].title)

      const togglePlay = () => {
        isPlaying.value = !isPlaying.value
      }

      const prevTrack = () => {
        if (currentTrackIndex.value > 0) currentTrackIndex.value--
        else currentTrackIndex.value = trackList.length - 1
      }

      const nextTrack = () => {
        if (currentTrackIndex.value < trackList.length - 1) currentTrackIndex.value++
        else currentTrackIndex.value = 0
      }

      const rewind = () => {
        console.log("Rewind clicked")
      }

      const forward = () => {
        console.log("Forward clicked")
      }

      const toggleMute = () => {
        isMuted.value = !isMuted.value
      }
      // 時間function
      const updateTime = () => {
        const now = new Date()
        currentTime.value = now.toLocaleTimeString('en-US', {
          hour: '2-digit', minute: '2-digit', hour12: true
        })
      }

      // 天氣
      const weatherList = [
        { condition: "Sunny", temperature: 25, icon: "sun.png" },
        { condition: "Cloudy Day", temperature: 20, icon: "cloudy.png" },
        { condition: "Light Rain", temperature: 18, icon: "rainy-day.png" },
        { condition: "Thunderstorm", temperature: 16, icon: "storm.png" },
        { condition: "Snowy Days", temperature: -2, icon: "snow.png" }
      ]
      const weather = ref(weatherList[0])
      const weatherImage = computed(() => require(`../assets/images/${weather.value.icon}`))

      const isButtonDisabled = ref(false)
      const showWeather = ref(true)
  
      const chooseRandomWeather = () => {
        isButtonDisabled.value = true
        setTimeout(() => {
          weather.value = weatherList[Math.floor(Math.random() * weatherList.length)]
          isButtonDisabled.value = false
        }, 2000)
      }
      const increaseTemperature = () => {
        sliderValue.value++
      }

      const decreaseTemperature = () => {
        sliderValue.value--
      }
      // 修改 PowerTemperature 函式：切換 needle 動畫和 AirConditionerIcon 狀態
    
      const PowerTemperature = () => {
        isNeedleAnimating.value = !isNeedleAnimating.value
        isAirConditionerOn.value = !isAirConditionerOn.value
      }
      // 利用 computed 依據 isAirConditionerOn 決定顯示哪個圖片
      const AirConditionerIcon = computed(() => {
        return isAirConditionerOn.value ? AirConditionerOpen : AirConditionerClose
      })
      // 控制風量
      const setSpeed = (speed) => {
        selectedSpeed.value = speed;
      }
      //切換 style
      const theme = ref('dark-theme');  // 默認主題
      const homeIcon = computed(() => {return isHomeIconBlack.value ? homeBlackIcon : homewhiteIcon})
       // 切換主題的方法
      const homeColorSwitch = () => {
        isHomeIconBlack.value =! isHomeIconBlack.value
        theme.value = isHomeIconBlack.value ? 'dark-theme' : 'light-theme';
        loadTheme();
      }
      // 加載主題樣式表
      const loadTheme = () => {
        const link = document.getElementById('theme-link');
        if (!link) {
          const head = document.head;
          const newLink = document.createElement('link');
          newLink.id = 'theme-link';
          newLink.rel = 'stylesheet';
          head.appendChild(newLink);
        }

        // 根據當前主題更新 CSS
        const currentTheme = theme.value === 'dark-theme' ? '/assets/DarkHomeControl.css' : '/assets/LigthHomeControl.css';
        document.getElementById('theme-link').href = currentTheme;
      };

      // 日期function
      onMounted(() => {
        loadTheme(); //CSS 主題
        updateTime()
        setInterval(updateTime, 60000)
        const today = new Date()
        const weekDays = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
        const weekDay = weekDays[today.getDay()]
        const month = today.toLocaleString('en-US', { month: 'long' })
        const day = today.getDate()
        fullDate.value = `${weekDay}, ${month} ${day}`        
      })
      return {
        ChevronDow,cdMusicImage,muteIcon,volumeIcon,volume,currentTrack, //音樂
        togglePlay,prevTrack,nextTrack,rewind,forward,toggleMute,isPlaying,isMuted, // 印月按鈕
        robotImage,
        fullDate, currentTime, weather, chooseRandomWeather,
        isButtonDisabled, showWeather, sliderValue,powerIcon,
        plusIcon,SubtractionIcon,increaseTemperature,decreaseTemperature,PowerTemperature,isNeedleAnimating,AirConditionerIcon, // 空調
        TimerIcon,leaftIcon,moonIcon,AirIcon,selectedSpeed,setSpeed,cycleIcon,WifiIcon,setingIcon, // 空調
        chartData,chartOptions,  //charts
        weatherImage, //天氣
        // OTHER
        CCTVIcon,CCTVSwitchOn, //CCTV
        LightBulbIcon,LightbulbSwitchOn, //LightBulb
        fanIcon,fanSwitchOn, //fan
        ExtensioncordIcon,ExtensioncordSwitchOn, // Extension cord
        homeIcon,homeColorSwitch,theme,//homeIcon
        //room
        hourseName: 'living room',
        hourseName1: 'Garage',
        hourseName2: 'Kitchen',
        hourseName3: 'Master Bedroom',
        hourseName4: 'Game room',
      }
    }
  }
</script>
