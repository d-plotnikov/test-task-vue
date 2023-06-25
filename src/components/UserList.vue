<template>
<div class="table-scroll mb-24">
    <div class="table-wrap">
        <table class="table">
            <thead>
                <tr>
                    <th class="table__head">Имя пользователя</th>
                    <th class="table__head">E-mail</th>
                    <th class="table__head">Дата регистрации</th>
                    <th class="table__head">Рейтинг</th>
                    <th class="table__head"></th>
                </tr>
            </thead>
            <tbody class="js-users">
                <tr v-for="user in users" :key="user.id">
                    <td class="table__username js-username">{{ user.username }}</td>
                    <td class="table__email js-email">{{ user.email }}</td>
                    <td class="table__date js-date">{{ user.registration_date.split('T')[0] }}</td>
                    <td class="table__rating js-rating">{{ user.rating }}</td>
                    <td class="table__close js-delete-item" @click="openModal(user.id)" >
                        <svg class="svg-icons">
                            <use xlink:href="./../assets/svg/sprite.svg#icon-close"></use>
                        </svg>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</div>
<div class="modal js-modal" v-if="modalActive">
    <div class="modal__card">
        <p class="modal__card-title">Вы уверены, что хотите удалить пользователя?</p>
        <div class="modal__card-buttons">
            <button class="btn js-modal-btn" @click="deleteItem()">Да</button>
            <button class="btn btn_blue js-modal-btn" @click="closeModal()">Нет</button>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'UserList',
    props: ['users', 'page'],
    data: function () {
        return {
            modalActive: false,
            userItems: [],
            id: 0,
        }
    },
    methods: {
        openModal(id) {
            this.id = id,
            this.modalActive = true
        },
        closeModal() {
            this.modalActive = false
        },
        deleteItem(){
            this.$emit('delete', this.id);
            if(this.users.length > 1) {
                this.$emit('page', this.page);
            } else {
                this.$emit('page', this.page - 1);
            }
            
            this.modalActive = false
        }
    },
}
</script>