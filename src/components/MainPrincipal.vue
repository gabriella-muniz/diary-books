<template>
  <div class="min-h-screen bg-gray-100 flex flex-col items-center py-6 px-4">
    <!-- Botão para abrir o modal -->
    <div class="w-full max-w-md mb-6 flex justify-center">
      <button
        @click="openModal"
        class="bg-blue-300 text-white px-4 py-2 rounded-md shadow-md hover:bg-blue-400 transition-colors"
      >
        Adicionar Livro
      </button>
    </div>

    <!-- Lista de Livros -->
    <div class="bg-white p-6 rounded-lg shadow-lg w-full max-w-4xl">
      <h1 class="text-2xl font-bold mb-4">Lista de Livros</h1>
      <ul>
        <li
          v-for="(book, index) in books"
          :key="index"
          class="flex flex-col mb-4 bg-gray-50 p-4 rounded-md shadow-sm"
        >
          <div class="flex flex-col md:flex-row items-center md:items-start space-y-4 md:space-y-0 md:space-x-4 mb-2">
            <img
              v-if="book.image"
              :src="book.image"
              alt="Capa do Livro"
              class="w-24 h-24 object-cover rounded-md mx-auto md:mx-0"
            />
            <div class="flex flex-col flex-grow text-center md:text-left">
              <h3 class="text-md font-medium text-gray-700 ">Nome:</h3>
              <h2 class="text-lg font-semibold">{{ book.name }}</h2>
              <h3 class="text-md font-medium text-gray-700 "> O que você achou: </h3>
              <p class="text-gray-600 break-words">
                {{ book.review }}
              </p>
              <p class="text-gray-500">Nota: {{ book.rating }}</p>
            </div>
          </div>
          <div class="flex space-x-2 justify-center md:justify-start">
            <button
              @click="editBook(index)"
              class="text-blue-500 hover:text-blue-700 transition-colors"
            >
              Editar
            </button>
            <button
              @click="removeBook(index)"
              class="text-red-500 hover:text-red-700 transition-colors"
            >
              Excluir
            </button>
          </div>
        </li>
      </ul>
    </div>

    <!-- Modal de Adicionar/Editar Livro -->
    <BookModal
      :isOpen="isModalOpen"
      :book="currentBook"
      :editingIndex="editingIndex"
      @submit="handleBookSubmit"
      @close="closeModal"
    />
  </div>
</template>

<script>
import BookModal from './BookModal.vue';

export default {
  components: {
    BookModal
  },
  data() {
    return {
      books: [],
      isModalOpen: false,
      currentBook: {},
      editingIndex: null
    };
  },
  methods: {
    openModal() {
      this.isModalOpen = true;
      this.currentBook = {};
      this.editingIndex = null;
    },
    closeModal() {
      this.isModalOpen = false;
    },
    addBook(book) {
      this.books.push(book);
    },
    editBook(index) {
      this.editingIndex = index;
      this.currentBook = { ...this.books[index] };
      this.isModalOpen = true;
    },
    handleBookSubmit(book, index) {
      if (index !== null) {
        this.books[index] = book;
      } else {
        this.addBook(book);
      }
      this.closeModal();
    },
    removeBook(index) {
      this.books.splice(index, 1);
    }
  }
};
</script>

<style scoped>
/* Estilos adicionais, se necessário */
</style>
