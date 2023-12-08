<template>
  <div class="container">
    <h1>Chatbot</h1>
    <section class="chat-box">
        <ul class="chat-box-list">
            <li class="msg">
                {{ steps[0].message }}
            </li>
            <li>
                <ul class="options">
                    <li class="msg" 
                      v-for="(option,index) in steps[1].options"
                      :key="index"
                      @click="nextQuestion(option)"
                      :class="option.selected"
                    >
                        {{ option.label }}
                    </li>
                </ul>
            </li>
          <li
            class="msg"
            v-for="(message, idx) in messages"
            :key="idx"
            :class="message.question"
          >
              {{ message.text }}
          </li>
        </ul>
    </section>
  </div>
</template>
  
  <script>
  export default {
    name: 'ChatBox',
    data: () => ({
      message: '',
      messages: [],
      steps: [
      {
        id: '1',
        message: 'Привет! Что я могу для Вас сделать?',
      },
      {
        id: '2',
        options: [
          { selected: '', label: 'Заказать пиццу', trigger: '3' },
          { selected: '', label: 'Установить будильник', trigger: '4' },
          { selected: '', label: 'Вывести погоду', trigger: '5' },
        ],
      },
      {
        id: '3',
        message: 'Хорошо, я закажу пиццу. Что еще могу сделать?',
      },
      {
        id: '4',
        message: 'Хорошо, я установлю будильник. Что еще могу сделать?',
      },
      {
        id: '5',
        message: 'Хорошо, я покажу погоду. Что еще могу сделать?',
      },
    ]
    }),
    methods: {
      nextQuestion(option) {
        option.selected = 'selected'
        this.steps[1].options.forEach(el => {
          if  (!el.selected)  {el.selected = 'unselected'}  
        });
        
        this.messages.push({
            text: this.steps[option.trigger-1].message,
            question: 'next'
          })
      }
    }
  }
  </script>
  
  <style scoped >
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  .container {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #777;
  padding-top: 60px;
}

  
  h1 {
    text-transform: uppercase;
    font-size: 1.5rem;
    margin: 1rem;
  }
  .chat-box {
    max-width: 500px;
    min-height: 50vh;
    margin: auto;
    border-radius: 20px;
    box-shadow: 0px 5px 10px 0px rgba(0, 0, 0, 0.5); 
  }
  li {
    list-style-type: none;
  }
  .chat-box-list {
    display: flex;
    flex-direction: column;
    padding: 1rem;
  }
  .msg {
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    width: 200px;
    margin: 10px;
    padding: 1rem;
    border-radius: 2rem 2rem 2rem 0;
    background: #7ba401;
    animation: ani 1s forwards;
    box-shadow: 0px 5px 10px 0px rgba(0, 0, 0, 0.3); 
  }

  @keyframes ani {
    0%, 80% {transform: translateX(-100%); opacity: 0;}
    100% {transform: translateY(0); opacity: 1;}
  }
  .options {
    display: flex;
  }
  .options .msg {
    font-size: clamp(14px, 3vw, 1rem);
    padding: 10px;
    margin: 5px;
    cursor: pointer;
    animation: ani 2s forwards;
  }
  .next {
    animation: ani 2s forwards;
  }
  .options .msg:hover {
    background: #99cc00;
  }
  .options .selected { 
    color: #333;
    font-size: 1rem;
    background: #fff;
    margin-left: auto;
    border: 1px solid #888;
    cursor: default;
    opacity: 0;
    animation: eni 2s forwards;
  }

  @keyframes eni {
    0% {opacity: 0;}
    100% {opacity: 1;}
  }
  .options .selected:hover {
    background: #fff;
  }
  .unselected {
    display: none;
  }
  </style>