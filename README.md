# rkalbumdesigninglet selectedCategory = '';
let selectedSize = '';

function selectCategory(categoryName, element) {
    selectedCategory = categoryName;
    selectedSize = ''; 
    const catButtons = document.querySelectorAll('.category-btn');
    catButtons.forEach(btn => btn.classList.remove('active'));
    element.classList.add('active');
    const sizeButtons = document.querySelectorAll('.size-btn');
    sizeButtons.forEach(btn => btn.classList.remove('active'));
    document.getElementById('sizesSection').style.display = 'block';
    document.getElementById('galleryGrid').innerHTML = '';
    document.getElementById('galleryTitle').innerText = categoryName.replace('-', ' ') + " -> Select a size";
}

function selectSize(sizeValue, element) {
    if (!selectedCategory) {
        alert("Please select a category first!");
        return;
    }
    selectedSize = sizeValue;
    const sizeButtons = document.querySelectorAll('.size-btn');
    sizeButtons.forEach(btn => btn.classList.remove('active'));
    element.classList.add('active');
    const formattedCategory = selectedCategory.replace('-', ' ');
    document.getElementById('galleryTitle').innerText = `${formattedCategory} — ${sizeValue} Designs`;
    renderImagesNoCode();
}

function renderImagesNoCode() {
    const galleryGrid = document.getElementById('galleryGrid');
    galleryGrid.innerHTML = '';
    const maxImagesToCheck = 20; 
    for (let i = 1; i <= maxImagesToCheck; i++) {
        const imageSrc = `images/${selectedCategory}/${selectedSize}/${i}.jpg`;
        const img = new Image();
        img.src = imageSrc;
        img.onload = function() {
            const card = document.createElement('div');
            card.className = 'gallery-item';
            card.innerHTML = `
                <img src="${imageSrc}" loading="lazy">
                <div class="item-info">
                    <h4>${selectedCategory.replace('-', ' ')} Design ${i}</h4>
                    <p>Size: ${selectedSize}</p>
                </div>
            `;
            galleryGrid.appendChild(card);
        };
    }
}
