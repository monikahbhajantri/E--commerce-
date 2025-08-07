/**
 * navbar toggle
 */

const overlay = document.querySelector("[data-overlay]");
const navOpenBtn = document.querySelector("[data-nav-open-btn]");
const navbar = document.querySelector("[data-navbar]");
const navCloseBtn = document.querySelector("[data-nav-close-btn]");

const navElemArr = [overlay, navOpenBtn, navCloseBtn];

for (let i = 0; i < navElemArr.length; i++) {
  navElemArr[i].addEventListener("click", function () {
    navbar.classList.toggle("active");
    overlay.classList.toggle("active");
  });
}



/**
 * add active class on header when scrolled 200px from top
 */

const header = document.querySelector("[data-header]");

window.addEventListener("scroll", function () {
  window.scrollY >= 200 ? header.classList.add("active")
    : header.classList.remove("active");
})


const productContainer = document.getElementById("productContainer");

fetch('https://fakestoreapi.com/products')
  .then(res => res.json())
  .then(products => {
    const filteredProducts = products.filter(product =>
      product.category === "men's clothing" ||
      product.category === "women's clothing" ||
      product.category === "jewelery"
    );

    filteredProducts.forEach(product => {
      const li = document.createElement("li");
      li.classList.add("product-item");

      li.innerHTML = `
        <div class="product-card">
          <figure class="card-banner">
            <img src="${product.image}" alt="${product.title}" class="image-contain" loading="lazy">
          </figure>

          <h3 class="h4 card-title">${product.title.slice(0, 30)}...</h3>

          <div class="card-price">
            <data value="${product.price}">₹ ${product.price}</data>
          </div>

          <button class="btn btn-primary">Buy Now</button>
        </div>
      `;

      productContainer.appendChild(li);
    });
  })
  .catch(err => {
    console.error("Failed to fetch products:", err);
  });
