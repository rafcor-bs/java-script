// Initialize an empty cart
let cart = [];

// Function to add items to the cart
function addToCart(service, price) {
    // Add item to the cart array
    cart.push({ service: service, price: price });

    // Update the cart display
    updateCartDisplay();
}

// Function to update the cart display
function updateCartDisplay() {
    // Get the cart items container
    const cartItemsContainer = document.getElementById('cart-items');

    // Clear the current cart display
    cartItemsContainer.innerHTML = '';

    // Loop through each item in the cart and create a list item
    cart.forEach(item => {
        const li = document.createElement('li');
        li.classList.add('list-group-item');
        li.textContent = `${item.service} - £${item.price}`;
        cartItemsContainer.appendChild(li);
    });

    // Calculate the total price of the cart
    const total = cart.reduce((sum, item) => sum + item.price, 0);
    const totalText = `Total: £${total}`;

    // Check if the total price element exists, if not, create one
    let totalElement = document.getElementById('cart-total');
    if (!totalElement) {
        totalElement = document.createElement('div');
        totalElement.id = 'cart-total';
        totalElement.innerHTML = `<h5>${totalText}</h5>`;
        document.getElementById('cart-summary').appendChild(totalElement);
    } else {
        totalElement.innerHTML = `<h5>${totalText}</h5>`;
    }
}

// Function to handle checkout
function checkout() {
    if (cart.length === 0) {
        alert('Your cart is empty!');
        return;
    }

    // Generate the cart details text
    let cartDetails = 'Items in your cart:\n';
    cart.forEach(item => {
        cartDetails += `${item.service} - £${item.price}\n`;
    });
    const total = cart.reduce((sum, item) => sum + item.price, 0);
    cartDetails += `\nTotal: £${total}`;

    // For this example, we just alert the cart items and total
    alert(cartDetails);

    // Optionally, you can clear the cart after checkout
    cart = [];
    updateCartDisplay();
}
