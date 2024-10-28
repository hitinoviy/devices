<template>
	<div className="devices">
		<div >
			<h3 className="devices__title" v-if="!ifEdited">{{ info.name }}</h3>
			<input 
				className="devices__title-change"
				v-if="ifEdited" 
				type="text" 
				v-model="inputChangeName" 
				placeholder="Новое название"
			/>
			<p class="error">{{ error }}</p>
			<ul className="devices__list">
				<li className="devices__item" v-for="(li, i) in info.nodes" :key="i">
					<p v-if="!ifEdited" >{{ li }}</p>
					
					<input 
						className="devices__item-input"
						v-if="ifEdited" 
						type="text" 
						v-model="info.nodes[i]" 
						placeholder="Новое название"
					/>
					<button className="devices__item-btn" v-if="ifEdited" @click="deleteNodes(i)">Удалить</button>
				</li>
				<div className="devices__wrapper" v-if="ifEdited">
					<input 
						className="devices__item-input"
						id="newNode" 
						v-model="newNode" 
						type="text"
						placeholder="Добавить новый узел"
					/>
					<button  className="devices__item-btn" @click="addNode">Добавить узел</button>
				</div>
			</ul>
		</div>

		<div >
			<button className="devices__item-btn" @click="deleteDevice(index)">Удалить</button>
			<button className="devices__item-btn" @click="editDevice">{{ ifEdited ? 'Сохранить' : 'Редактировать' }}</button>
		</div>
  </div>
</template>

<script>
export default {
	data() {
		return {
			newNode: '',
			error: '',
			ifEdited: false,
			inputChangeName: this.info.name 
		}
	},
	props: {
		info: {
			type: Object,
			required: true
		},
		index: {
			type: Number,
			required: true
		},
		deleteDevice: {
			type: Function,
			required: true
		}
	},
	methods: {
        editDevice() {
            this.ifEdited = !this.ifEdited;
            if (this.ifEdited) {
                this.inputChangeName = this.info.name;
            }
        },
        deleteNodes(index) {
            this.info.nodes.splice(index, 1);
        },
        addNode() {
            if (!this.newNode) {
                this.error = 'Вы не ввели название узла';
                console.log(this.error);
                return;
            }
            this.error = ''; 
            this.info.nodes.push(this.newNode); 
            this.newNode = ''; 
        }
    }
}
</script>

<style scoped src="/src/assets/style/deviceItem.css">

</style>