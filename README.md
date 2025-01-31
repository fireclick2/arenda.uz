<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>arenda.uz - Аренда и продажа квартир</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f9;
    }

    header {
      background-color: #007bff;
      color: white;
      padding: 10px 20px;
      text-align: center;
    }

    header nav a {
      color: white;
      margin: 0 10px;
      text-decoration: none;
    }

    main {
      padding: 20px;
    }

    section {
      margin-bottom: 40px;
    }

    #search input, #listing-form input, #listing-form textarea {
      display: block;
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    #search button, #listing-form button {
      padding: 10px 20px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    #search button:hover, #listing-form button:hover {
      background-color: #0056b3;
    }

    #apartment-list {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 20px;
    }

    .apartment {
      background: white;
      padding: 15px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <header>
    <h1>arenda.uz</h1>
    <nav>
      <a href="#listings">Объявления</a>
      <a href="#add-listing">Добавить объявление</a>
    </nav>
  </header>

  <main>
    <section id="search">
      <h2>Поиск квартиры</h2>
      <input type="text" id="search-input" placeholder="Введите город, район или название...">
      <button id="search-btn">Найти</button>
    </section>

    <section id="listings">
      <h2>Объявления</h2>
      <div id="apartment-list">
        <!-- Здесь будут выводиться объявления -->
      </div>
    </section>

    <section id="add-listing">
      <h2>Добавить объявление</h2>
      <form id="listing-form">
        <input type="text" id="title" placeholder="Заголовок" required>
        <input type="text" id="location" placeholder="Город/Район" required>
        <input type="number" id="price" placeholder="Цена ($)" required>
        <textarea id="description" placeholder="Описание" required></textarea>
        <button type="submit">Добавить</button>
      </form>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 arenda.uz</p>
  </footer>

  <script>
    document.addEventListener("DOMContentLoaded", () => {
      const apartmentList = document.getElementById("apartment-list");
      const listingForm = document.getElementById("listing-form");

      // Массив для хранения объявлений
      let listings = [];

      // Функция для отображения объявлений
      function renderListings() {
        apartmentList.innerHTML = "";
        listings.forEach((listing, index) => {
          const apartmentDiv = document.createElement("div");
          apartmentDiv.classList.add("apartment");
          apartmentDiv.innerHTML = 
            <h3>${listing.title}</h3>
            <p><strong>Местоположение:</strong> ${listing.location}</p>
            <p><strong>Цена:</strong> $${listing.price}</p>
            <p>${listing.description}</p>
            <button onclick="deleteListing(${index})">Удалить</button>
          ;
          apartmentList.appendChild(apartmentDiv);
        });
      }

      // Обработчик отправки формы
      listingForm.addEventListener("submit", (event) => {
        event.preventDefault();
        const title = document.getElementById("title").value;
        const location = document.getElementById("location").value;
        const price = document.getElementById("price").value;
        const description = document.getElementById("description").value;

        listings.push({ title, location, price, description });
        renderListings();

        listingForm.reset();
      });
// Функция для удаления объявления
      window.deleteListing = (index) => {
        listings.splice(index, 1);
        renderListings();
      };
    });
  </script>
</body>
</html>
