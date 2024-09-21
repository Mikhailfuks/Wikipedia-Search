const searchInput = document.getElementById('search-input');
const searchButton = document.getElementById('search-button');
const resultsContainer = document.getElementById('results');

searchButton.addEventListener('click', searchWikipedia);

function searchWikipedia() {
  const query = searchInput.value.trim();
  if (query === '') {
    alert('Please enter a search term.');
    return;
  }

  const apiUrl = https://en.wikipedia.org/w/api.php?action=opensearch&search=${query}&format=json&limit=10;

  fetch(apiUrl)
    .then(response => response.json())
    .then(data => displayResults(data))
    .catch(error => {
      console.error('Error fetching data:', error);
      displayError('An error occurred while searching. Please try again later.');
    });
}

function displayResults(data) {
  resultsContainer.innerHTML = ''; // Clear previous results

  if (data[1].length === 0) {
    displayError('No results found.');
    return;
  }

  data[1].forEach((title, index) => {
    const resultLink = document.createElement('a');
    resultLink.href = data[3][index];
    resultLink.textContent = title;
    resultsContainer.appendChild(resultLink);
    resultsContainer.appendChild(document.createElement('br'));
  });
}

function displayError(message) {
  const errorElement = document.createElement('p');
  errorElement.textContent = message;
  errorElement.classList.add('error');
  resultsContainer.appendChild(errorElement);
}

// HTML Structure (index.html)
// Add this within your <body> tag:
