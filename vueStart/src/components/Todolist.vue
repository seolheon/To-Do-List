<template>
    <div class="todo-list-container">
        <section class="add-task-bar">
            <input v-model="inputValue" class="add-task" type="text" placeholder="Enter task" @keydown.enter="createTask"/>
            <div @click="createTask" class="add-button">
                <svg class="add-icon" width="25" height="26" viewBox="0 0 25 26" fill="#606060" xmlns="http://www.w3.org/2000/svg">
                    <path d="M12.5 0.745117C10.0277 0.745117 7.61099 1.46385 5.55538 2.81044C3.49976 4.15703 1.89761 6.07098 0.951511 8.31027C0.00541605 10.5496 -0.242126 13.0136 0.24019 15.3908C0.722505 17.768 1.91301 19.9517 3.66117 21.6655C5.40933 23.3794 7.63661 24.5466 10.0614 25.0194C12.4861 25.4923 14.9995 25.2496 17.2835 24.3221C19.5676 23.3945 21.5199 21.8238 22.8934 19.8085C24.2669 17.7932 25 15.4238 25 13C25 11.3907 24.6767 9.7971 24.0485 8.31027C23.4203 6.82344 22.4996 5.47247 21.3388 4.33449C20.1781 3.19652 18.8001 2.29383 17.2835 1.67797C15.767 1.0621 14.1415 0.745117 12.5 0.745117ZM12.5 22.8039C10.5222 22.8039 8.58879 22.2289 6.9443 21.1517C5.29981 20.0744 4.01809 18.5432 3.26121 16.7518C2.50433 14.9604 2.3063 12.9891 2.69215 11.0874C3.078 9.18559 4.03041 7.4387 5.42894 6.0676C6.82746 4.6965 8.60929 3.76276 10.5491 3.38448C12.4889 3.00619 14.4996 3.20034 16.3268 3.94238C18.1541 4.68441 19.7159 5.941 20.8147 7.55325C21.9135 9.1655 22.5 11.061 22.5 13C22.5 15.6002 21.4464 18.0938 19.5711 19.9324C17.6957 21.771 15.1522 22.8039 12.5 22.8039ZM17.5 11.7745H13.75V8.09806C13.75 7.77304 13.6183 7.46133 13.3839 7.2315C13.1495 7.00168 12.8315 6.87257 12.5 6.87257C12.1685 6.87257 11.8505 7.00168 11.6161 7.2315C11.3817 7.46133 11.25 7.77304 11.25 8.09806V11.7745H7.5C7.16848 11.7745 6.85054 11.9036 6.61612 12.1335C6.3817 12.3633 6.25 12.675 6.25 13C6.25 13.325 6.3817 13.6367 6.61612 13.8666C6.85054 14.0964 7.16848 14.2255 7.5 14.2255H11.25V17.902C11.25 18.227 11.3817 18.5387 11.6161 18.7685C11.8505 18.9984 12.1685 19.1275 12.5 19.1275C12.8315 19.1275 13.1495 18.9984 13.3839 18.7685C13.6183 18.5387 13.75 18.227 13.75 17.902V14.2255H17.5C17.8315 14.2255 18.1495 14.0964 18.3839 13.8666C18.6183 13.6367 18.75 13.325 18.75 13C18.75 12.675 18.6183 12.3633 18.3839 12.1335C18.1495 11.9036 17.8315 11.7745 17.5 11.7745Z"/>
                </svg>
            </div>

            <div class="filter-button" @mouseover="isMenuOpen=true" @mouseleave="isMenuOpen=false">
                <svg class="filter-icon" width="25" height="26" viewBox="0 0 25 26" fill="#606060" xmlns="http://www.w3.org/2000/svg">
                    <path d="M21.25 0.725464H3.75C2.75544 0.725464 1.80161 1.11281 1.09835 1.80228C0.395088 2.49175 2.26098e-07 3.42687 2.26098e-07 4.40193V5.83576C-0.000179009 6.34181 0.106208 6.84246 0.3125 7.30634V7.37987C0.4891 7.77322 0.73924 8.13068 1.05 8.4338L8.75 15.9338V24.0098C8.74957 24.218 8.80329 24.423 8.90609 24.6052C9.00888 24.7875 9.15736 24.9411 9.3375 25.0514C9.53642 25.1723 9.76597 25.236 10 25.2353C10.1957 25.2341 10.3883 25.1879 10.5625 25.1005L15.5625 22.6495C15.7686 22.5476 15.942 22.3918 16.0633 22.1993C16.1847 22.0068 16.2493 21.7851 16.25 21.5588V15.9338L23.9 8.4338C24.2108 8.13068 24.4609 7.77322 24.6375 7.37987V7.30634C24.861 6.84609 24.9845 6.34529 25 5.83576V4.40193C25 3.42687 24.6049 2.49175 23.9016 1.80228C23.1984 1.11281 22.2446 0.725464 21.25 0.725464ZM14.1125 14.5612C13.9966 14.6758 13.905 14.8116 13.8428 14.9609C13.7806 15.1102 13.749 15.2701 13.75 15.4313V20.799L11.25 22.0245V15.4313C11.2509 15.2701 11.2194 15.1102 11.1572 14.9609C11.095 14.8116 11.0033 14.6758 10.8875 14.5612L4.2625 8.0784H20.7375L14.1125 14.5612ZM22.5 5.62742H2.5V4.40193C2.5 4.07691 2.6317 3.76521 2.86612 3.53538C3.10054 3.30556 3.41848 3.17644 3.75 3.17644H21.25C21.5815 3.17644 21.8995 3.30556 22.1339 3.53538C22.3683 3.76521 22.5 4.07691 22.5 4.40193V5.62742Z"/>
                </svg>
                <div v-show="isMenuOpen" class="filter-menu" @mouseover.stop>
                    <div :class="filterFlag === 'all' ? 'active' : 'button'"  @click="setFilter('all')">All</div>
                    <div :class="filterFlag === 'important' ? 'active' : 'button'"  @click="setFilter('important')">Important</div>
                    <div :class="filterFlag === 'completed' ? 'active' : 'button'"  @click="setFilter('completed')">Completed</div>
                    <div :class="filterFlag === 'uncompleted' ? 'active' : 'button'"  @click="setFilter('uncompleted')">Uncompleted</div>
                </div>
            </div>
        </section>
        <ul class="task-list">
            <li v-for="task in getFilteredTasks" :key="task.id" class="todo-item" >
              <div class="todo-item-content" :class="{ 'important':task.isImportant & !task.isComplete, 'completed': task.isComplete }">
                <p v-if="!task.isEdit" class="todo-item-text" >
                  {{ task.description }}
                </p>
                <input v-else class="edit-task" v-model="task.description" type="text"/>
                <div class="todo-item-actions">
                    <div v-show="!task.isComplete" class="edit-button" @click = "task.isEdit = !task.isEdit" >
                        <svg v-show="!task.isEdit" class="edit-icon" width="25" height="25" viewBox="0 0 25 25" fill="#404040" xmlns="http://www.w3.org/2000/svg">
                            <path d="M25 6.54953C25.0009 6.38504 24.9694 6.22197 24.9072 6.06968C24.845 5.9174 24.7533 5.77889 24.6375 5.6621L19.3375 0.362494C19.2207 0.246651 19.0822 0.155001 18.9299 0.0927999C18.7776 0.0305988 18.6145 -0.000930154 18.45 2.08913e-05C18.2855 -0.000930154 18.1224 0.0305988 17.9701 0.0927999C17.8178 0.155001 17.6793 0.246651 17.5625 0.362494L0.36252 17.5612C0.246669 17.678 0.155012 17.8165 0.0928067 17.9688C0.030601 18.1211 -0.000930222 18.2841 2.08928e-05 18.4486V23.7482C2.08928e-05 24.0797 0.131717 24.3977 0.366137 24.6321C0.600557 24.8665 0.918499 24.9982 1.25002 24.9982H6.55001C6.72492 25.0077 6.89988 24.9803 7.06353 24.9179C7.22719 24.8554 7.3759 24.7593 7.50001 24.6357L21.0875 10.9742L24.6375 7.49946C24.7516 7.37832 24.8445 7.2389 24.9125 7.08699C24.9245 6.98736 24.9245 6.88664 24.9125 6.78701C24.9183 6.72883 24.9183 6.67021 24.9125 6.61203L25 6.54953ZM6.03751 22.4983H2.50002V18.9611L14.9125 6.54953L18.45 10.0868L6.03751 22.4983ZM20.2125 8.3244L16.675 4.78716L18.45 3.0248L21.975 6.54953L20.2125 8.3244Z"/>
                        </svg>

                        <svg v-show="task.isEdit" class="save-icon" width="26" height="26" viewBox="0 0 26 26" fill="#404040" xmlns="http://www.w3.org/2000/svg">
                            <path d="M25.0892 8.91083L16.5892 0.410833C16.4586 0.283403 16.3047 0.182386 16.1358 0.113333C15.9602 0.0419573 15.7729 0.00353894 15.5833 0H4.25C3.12283 0 2.04183 0.447767 1.2448 1.2448C0.447767 2.04183 0 3.12283 0 4.25V21.25C0 22.3772 0.447767 23.4582 1.2448 24.2552C2.04183 25.0522 3.12283 25.5 4.25 25.5H21.25C22.3772 25.5 23.4582 25.0522 24.2552 24.2552C25.0522 23.4582 25.5 22.3772 25.5 21.25V9.91667C25.5011 9.73022 25.4653 9.5454 25.3948 9.3728C25.3243 9.2002 25.2205 9.04321 25.0892 8.91083ZM8.5 2.83333H14.1667V5.66667H8.5V2.83333ZM17 22.6667H8.5V18.4167C8.5 18.0409 8.64926 17.6806 8.91493 17.4149C9.18061 17.1493 9.54094 17 9.91667 17H15.5833C15.9591 17 16.3194 17.1493 16.5851 17.4149C16.8507 17.6806 17 18.0409 17 18.4167V22.6667ZM22.6667 21.25C22.6667 21.6257 22.5174 21.9861 22.2517 22.2517C21.9861 22.5174 21.6257 22.6667 21.25 22.6667H19.8333V18.4167C19.8333 17.2895 19.3856 16.2085 18.5885 15.4115C17.7915 14.6144 16.7105 14.1667 15.5833 14.1667H9.91667C8.7895 14.1667 7.70849 14.6144 6.91146 15.4115C6.11443 16.2085 5.66667 17.2895 5.66667 18.4167V22.6667H4.25C3.87428 22.6667 3.51394 22.5174 3.24827 22.2517C2.98259 21.9861 2.83333 21.6257 2.83333 21.25V4.25C2.83333 3.87428 2.98259 3.51394 3.24827 3.24827C3.51394 2.98259 3.87428 2.83333 4.25 2.83333H5.66667V7.08333C5.66667 7.45906 5.81592 7.81939 6.0816 8.08507C6.34728 8.35074 6.70761 8.5 7.08333 8.5H15.5833C15.9591 8.5 16.3194 8.35074 16.5851 8.08507C16.8507 7.81939 17 7.45906 17 7.08333V4.83083L22.6667 10.4975V21.25Z" />
                        </svg>
                    </div>

                    <div v-show="!task.isComplete & !task.isEdit" class="important-button" @click="toggleImportant(task)">
                        <svg class="important-icon" width="28" height="28" viewBox="0 0 28 28" fill = "none" stroke="#404040" stroke-width="2" xmlns="http://www.w3.org/2000/svg">
                            <path d="M15.9224 3.07343C15.3682 1.14237 12.6318 1.14237 12.0776 3.07343L10.1683 9.72618L3.25121 9.48618C1.24341 9.41651 0.397809 12.019 2.0631 13.1428L7.80026 17.0144L5.43448 23.5188C4.74778 25.4068 6.96159 27.0153 8.54499 25.7788L14 21.5188L19.455 25.7788C21.0384 27.0153 23.2522 25.4068 22.5655 23.5188L20.1997 17.0144L25.9369 13.1428C27.6022 12.019 26.7566 9.41651 24.7488 9.48618L17.8317 9.72618L15.9224 3.07343Z"/>
                        </svg>
                    </div>

                    <div v-show="!task.isEdit" class="checkbox" @click="toggleComplete(task)">

                        <svg v-show="!task.isComplete" class="checkbox-icon" width="28" height="28" viewBox="0 0 28 28" fill="none" stroke="#404040" stroke-width="2" xmlns="http://www.w3.org/2000/svg">
                            <rect x="1" y="1" width="25" height="25" rx="3" />
                        </svg>

                        <svg v-show="task.isComplete" class="confirm-icon" width="28" height="28" viewBox="0 0 28 28" fill="#606060" xmlns="http://www.w3.org/2000/svg">
                            <path d="M22.4205 5.74463C22.576 5.82796 22.717 5.95006 22.8356 6.10389C22.9651 6.25758 23.0684 6.44411 23.1391 6.65173C23.2098 6.85935 23.2463 7.08356 23.2463 7.31022C23.2463 7.53688 23.2098 7.76108 23.1391 7.9687C23.0684 8.17632 22.9651 8.36285 22.8356 8.51655L12.4266 21.9092C12.308 22.0631 12.1669 22.1852 12.0115 22.2685C11.856 22.3518 11.6893 22.3947 11.5209 22.3947C11.3525 22.3947 11.1858 22.3518 11.0303 22.2685C10.8749 22.1852 10.7338 22.0631 10.6152 21.9092L5.71686 15.6068C5.59374 15.4538 5.49525 15.271 5.42701 15.069C5.35877 14.867 5.32213 14.6497 5.31916 14.4295C5.3162 14.2093 5.34698 13.9904 5.40975 13.7855C5.47252 13.5806 5.56604 13.3936 5.68497 13.2352C5.80391 13.0768 5.94593 12.95 6.10293 12.8622C6.25993 12.7744 6.42884 12.7273 6.6 12.7235C6.77116 12.7197 6.94123 12.7593 7.1005 12.84C7.25977 12.9208 7.40511 13.0411 7.52824 13.1941L11.5209 18.3477L21.0243 6.10389C21.1428 5.95006 21.2839 5.82796 21.4394 5.74463C21.5948 5.66131 21.7615 5.61841 21.9299 5.61841C22.0983 5.61841 22.2651 5.66131 22.4205 5.74463Z"/>
                            <path fill-rule="evenodd" clip-rule="evenodd" d="M4.33514 0.671082C2.12601 0.671082 0.335144 2.46194 0.335144 4.67108V23.3421C0.335144 25.5513 2.12601 27.3421 4.33515 27.3421H23.2342C25.4433 27.3421 27.2342 25.5513 27.2342 23.3421V4.67108C27.2342 2.46194 25.4433 0.671082 23.2342 0.671082H4.33514ZM2.33514 4.67108C2.33514 3.56651 3.23057 2.67108 4.33514 2.67108H23.2342C24.3388 2.67108 25.2342 3.56651 25.2342 4.67108V23.3421C25.2342 24.4467 24.3388 25.3421 23.2342 25.3421H4.33515C3.23058 25.3421 2.33514 24.4467 2.33514 23.3421V4.67108Z"/>        
                        </svg>

                    </div>
                </div>
              </div>

              <div class="remove-button" @click="deleteTask(task.id)">
                <svg class="remove-icon" width="16" height="16" viewBox="0 0 16 16" fill="#353535" xmlns="http://www.w3.org/2000/svg">
                    <path d="M9.87818 7.99886L15.606 2.28357C15.8568 2.03271 15.9977 1.69246 15.9977 1.33769C15.9977 0.98291 15.8568 0.642664 15.606 0.391799C15.3552 0.140935 15.015 0 14.6602 0C14.3055 0 13.9653 0.140935 13.7145 0.391799L8 6.12041L2.28552 0.391799C2.03469 0.140935 1.6945 -2.64329e-09 1.33977 0C0.985044 2.64329e-09 0.644846 0.140935 0.394017 0.391799C0.143188 0.642664 0.00227327 0.98291 0.00227327 1.33769C0.00227327 1.69246 0.143188 2.03271 0.394017 2.28357L6.12182 7.99886L0.394017 13.7142C0.269166 13.838 0.17007 13.9853 0.102444 14.1477C0.0348177 14.31 0 14.4842 0 14.66C0 14.8359 0.0348177 15.01 0.102444 15.1724C0.17007 15.3347 0.269166 15.4821 0.394017 15.6059C0.517848 15.7308 0.665174 15.8299 0.827496 15.8975C0.989818 15.9652 1.16392 16 1.33977 16C1.51562 16 1.68972 15.9652 1.85204 15.8975C2.01437 15.8299 2.16169 15.7308 2.28552 15.6059L8 9.87731L13.7145 15.6059C13.8383 15.7308 13.9856 15.8299 14.148 15.8975C14.3103 15.9652 14.4844 16 14.6602 16C14.8361 16 15.0102 15.9652 15.1725 15.8975C15.3348 15.8299 15.4822 15.7308 15.606 15.6059C15.7308 15.4821 15.8299 15.3347 15.8976 15.1724C15.9652 15.01 16 14.8359 16 14.66C16 14.4842 15.9652 14.31 15.8976 14.1477C15.8299 13.9853 15.7308 13.838 15.606 13.7142L9.87818 7.99886Z" />
                </svg>
              </div>
            </li>
        </ul>
      </div>
</template>
  
<script setup>
    import { ref, computed } from 'vue'
    const isMenuOpen = ref(false);
    const importantTasks = ref([]);
    const completedTasks = ref([]);
    const todoList = ref([
        {
            id: 0,
            description: 'Design',
            isEdit: false,
            isComplete: false,
            isImportant: false,
        },
        {
            id: 1,
            description: 'Layout',
            isEdit: false,
            isComplete: false,
            isImportant: false,
        },
        {
            id: 2,
            description: 'Function',
            isEdit: false,
            isComplete: false,
            isImportant: false,
        }
    ])

    const moveItem = (arr, fromIndex, toIndex) => {
    arr.splice(toIndex, 0, arr.splice(fromIndex, 1)[0]);
  };

  const toggleComplete = (task) => {

    task.isComplete = !task.isComplete;
    if (task.isComplete) {

        if (task.isImportant){
            const index = importantTasks.value.indexOf(task);
            importantTasks.value.splice(index, 1);
            completedTasks.value.push(task);
        }
        else{
            const index = todoList.value.indexOf(task);
            todoList.value.splice(index, 1);
            completedTasks.value.push(task);
        }
    } else {

        if (task.isImportant){
            const index = completedTasks.value.indexOf(task);
            completedTasks.value.splice(index, 1);
            importantTasks.value.unshift(task);
        }
        else{
            const index = completedTasks.value.indexOf(task);
            completedTasks.value.splice(index, 1);
            todoList.value.push(task);
        }
    }
};

const toggleImportant = (task) => {
    task.isImportant = !task.isImportant;
    if (task.isImportant) {
        const index = todoList.value.indexOf(task);
        todoList.value.splice(index, 1);
        importantTasks.value.unshift(task);
    } else {
        const index = importantTasks.value.indexOf(task);
        importantTasks.value.splice(index, 1);
        todoList.value.unshift(task);
    }
};

const getSortedTasks = () => {
    const sortedTasks = [];
    sortedTasks.push(...importantTasks.value);
    sortedTasks.push(...todoList.value.filter(task => !importantTasks.value.includes(task) && !completedTasks.value.includes(task)));
    sortedTasks.push(...completedTasks.value);
    return sortedTasks;
};

const filterFlag = ref('all');

const setFilter = (filter) => {
      filterFlag.value = filter;
    };

const getFilteredTasks = computed(() => {
    const sortedTasks = getSortedTasks();
    switch (filterFlag.value) {
      case 'all':
        return sortedTasks;
      case 'important':
        return importantTasks.value;
      case 'completed':
        return completedTasks.value;
      case 'uncompleted':
        return todoList.value;
      default:
        return sortedTasks;
    }
  });


    const deleteTask = (id) => {
        todoList.value = todoList.value.filter(el => el.id != id);
        importantTasks.value = importantTasks.value.filter(el => el.id != id);
        completedTasks.value = completedTasks.value.filter(el => el.id != id);
    }

    const inputValue = ref('') 

    const createTask = () => {
        const newTask = {
            id: Date.now(),
            description: inputValue.value,
            isEdit: false,
            isComplete: false,
            isImportant: false,
        }
        if (inputValue.value !== ''){
            todoList.value.push(newTask)
            inputValue.value = '';
        }
    }

</script>
  
  <style scoped>
  .todo-list-container {
    border-radius: 35px;
    background-color: #282828;
    display: flex;
    flex-direction: column;
    padding: 30px 40px;
    box-shadow: 0px 0px 7px 5px rgba(0, 0, 0, 0.5);
    user-select: none;
  }

  .add-task-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
  }

  .add-task {
    border-radius: 15px;
    background-color: #202020;
    width: 520px;
    height: 50px;
    color: #808080;
    border: none;
    padding-left: 2%;
    box-shadow: 0px 0px 0px 1px rgba(0, 0, 0, 0.3);
  }

  .edit-task {
    border-radius: 5px;
    background-color: #404040;
    height: 25px;
    color: #000000;
    box-shadow: none;
    border: none;
    flex-grow: 1;
    padding-left: 2%;
  }

  .add-task:focus,
  .edit-task:focus {
    outline: none;
    transition: box-shadow 0.3s ease;
    box-shadow: 0px 0px 0px 1px rgba(255, 255, 255, 0.5);
}

.add-task:hover,
.edit-task:hover {
    outline: none;
    transition: box-shadow 0.3s ease;
    box-shadow: 0px 0px 0px 1px rgba(255, 255, 255, 0.3);
}
  
  .add-button,
  .filter-button {
    width: 75px;
    height: 50px;
    background-color: #202020;
    border-radius: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    box-shadow: 0px 0px 0px 1px rgba(0, 0, 0, 0.2);
  }

  .edit-button:hover svg, 
  .add-button:hover svg,
  .filter-button:hover svg {
    transition: fill 0.3s ease;
    fill: #fff;
  }

  .add-button:hover,
  .filter-button:hover{
    transition: box-shadow 0.3s ease;
    box-shadow: 0px 0px 0px 1px rgba(255, 255, 255, 0.2);

  }

  .filter-menu {
     display: flex;
     flex-direction: column;
     justify-content: center;
     position: absolute;
     background-color: #151515;
     border: 1px solid #000;
     border-radius: 4px;
     padding: 15px;
     gap: 10px;
     z-index: 1;
     left: 50px;
     box-shadow: 0px 0px 5px 2px rgba(0, 0, 0, 0.5);
    }

    .filter-menu .button {
     background-color: #404040;
     border: 1px solid #000;
     border-radius: 4px;
     text-align: center;
     padding: 10px;
     color: #fff;
     font-weight: 600;
     font: 500 16px Montserrat Alternates, -apple-system, Roboto, Helvetica, sans-serif;
    }

    .filter-menu .button:hover {
     transition: background-color 0.3s ease;
     background-color: #202020;
     color: #fff;
    }

  .important-button :hover ,
  .checkbox :hover, 
  .important .checkbox :hover {
    transition: stroke 0.3s ease;
    stroke: #fff;
  }

  .checkbox .confirm-icon:hover {
    transition: fill 0.3s ease;
    fill: #fff;
  }

  .edit-button, 
  .important-button,
  .checkbox {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .task-list{
    padding: 0px;
    margin-top: 0px;
    margin-bottom: 0px;
  }

  .todo-item {
    display: flex;
    gap: 0;
    margin-top: 20px;
  }
  
  .todo-item-content {
    border-radius: 10px 0 0 10px;
    background-color: #202020;
    gap: 20px;
    flex-grow: 1;
    padding: 25px 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    font: 500 16px Montserrat Alternates, -apple-system, Roboto, Helvetica, sans-serif;
  }
  
  .todo-item-text {
    color: rgba(255, 255, 255, 0.59);
    flex-grow: 1;
    margin: 0;
  }
  
  .todo-item-actions {
    display: flex;
    gap: 15px;
    align-self: right;
  }

  .remove-button {
    border-radius: 0 10px 10px 0;
    background-color: #404040;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 35px
  }

  .remove-button:hover {
    transition: background-color 0.5s ease;
    background-color: #B07171;
  }

  .remove-button:hover svg{
    transition: fill 0.5s ease;
    fill: #8e5151;
  }

    .completed .todo-item-text {
    text-decoration: line-through;
    color: #000000;
    font-weight: 400;
  }

  .completed {
    background-color: #353535;
  }

  .important .important-icon {
    fill: #ccc591;
    stroke: none;
  }

  .important .checkbox-icon,
  .important .confirm-icon  {
    stroke: #202020;
  }

  .important .edit-icon, 
  .important .save-icon {
    fill: #202020;
  }

  .important  {
    background-color: #71988b;
  }

  .important .todo-item-text  {
    color: #202020;
    font-weight: 600;
  }

  .important .edit-task  {
    color: #202020;
    background-color: #add9ca;
    font-weight: 600;
  }

  .important ~.remove-button {
    background-color: #336a57;
  }

  .important ~.remove-button svg {
    fill: #2c5749;
  }

  .important ~.remove-button:hover svg {
    fill: #915954;
  }

  .important ~.remove-button:hover {
    background-color: #b3716b;
  }

  .important .important-button :hover {
    transition: fill 0.2s ease;
    fill: #f3ecb3;
    stroke: none;
  } 

  .active {
    background-color: #202020;
     border: 1px solid #000;
     border-radius: 4px;
     text-align: center;
     padding: 10px;
     color: #8b8b8b;
     font-weight: 600;
     font: 500 16px Montserrat Alternates, -apple-system, Roboto, Helvetica, sans-serif;
  }

  .add-button:active,
  .filter-button:active {
    transition: background-color 4s ease;
    background-color: #181818;
    transition: box-shadow 4s ease;
    box-shadow: none;
    transition: transform 4s ease;
    transform: translateY(5px);
  }

</style>