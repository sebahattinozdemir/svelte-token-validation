<script>
    import { onMount } from 'svelte';
  
    let telegramID = '';
    let maskedPassword = '';
    let createdAt = '';
    let userData = {};
  
    // Mask the password except the first character
    function maskPassword(password) {
      return password[0] + '*'.repeat(password.length - 1);
    }
  
    // Check if the user is logged in and display account info
    onMount(() => {
      const isLoggedIn = localStorage.getItem('isLoggedIn');
      const savedUserData = localStorage.getItem('userData');
  
      if (isLoggedIn !== 'true' || !savedUserData) {
        alert('You need to sign up or log in.');
        window.location.href = '/'; // Redirect to Sign-Up page if not logged in or user data not found
      }
  
      // Load user data
      userData = JSON.parse(savedUserData);
      telegramID = userData.telegramID;
      maskedPassword = maskPassword(userData.password);
      createdAt = new Date(userData.createdAt).toLocaleDateString();
    });
  </script>
  
  <main class="min-h-screen bg-gray-100 flex items-center justify-center">
    <div class="bg-white p-8 rounded-lg shadow-md w-full max-w-md">
      <h1 class="text-2xl font-bold mb-6 text-center">Profile</h1>
  
      <div class="bg-gray-100 border border-gray-300 px-4 py-3 rounded mb-4">
        <p><strong>{telegramID}</strong> {maskedPassword}</p>
        <p class="mt-2">Created: {createdAt}</p>
      </div>
    </div>
  </main>
  