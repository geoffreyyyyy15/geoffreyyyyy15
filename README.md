<!DOCTYPE html>
<html>
  <head>
    <title>Display Most Used Languages in GitHub README</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  </head>
  <body>
    <h1>Most Used Languages in README</h1>
    <div id="languages"></div>
    <script>
      const repoUrl = 'https://github.com/geoffreyyyyy15/Socialites_Appointment_System'; // Replace with your repo URL
      
      // Fetch the repository information
      axios.get(repoUrl).then(function(response) {
        const repo = response.data;
        
        // Get the language statistics
        const languages = repo.languages_url;
        axios.get(languages).then(function(response) {
          const langData = response.data;
          
          // Sort the languages by usage count
          const sortedLangs = Object.keys(langData).sort(function(a, b) {
            return langData[b] - langData[a];
          });
          
          // Display the top 5 languages
          const topLangs = sortedLangs.slice(0, 5);
          const languagesDiv = document.getElementById('languages');
          topLangs.forEach(function(lang) {
            const langDiv = document.createElement('div');
            langDiv.textContent = lang + ': ' + langData[lang];
            languagesDiv.appendChild(langDiv);
          });
        });
      });
    </script>
  </body>
</html>

This code uses the Axios library to fetch the repository information and language statistics from the GitHub API. The languages are sorted by usage count using the sort() method, and the top 5 languages are displayed in a div element with an ID of "languages".

You'll need to replace the "owner/repo" part of the repoUrl variable with the owner and repository name of the GitHub repository you want to display the languages for.
