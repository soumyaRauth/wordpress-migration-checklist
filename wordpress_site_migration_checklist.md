When migrating a WordPress site to a new address, there are several steps to ensure everything works properly. Here's a checklist to help troubleshoot why the site might not be working after migration:

1. **Database Search and Replace:**
   - Even after updating `wp-options`, there might be instances of the old site URL in the database. You should perform a search and replace in the database to update any hardcoded URLs. You can use a plugin like "Better Search Replace" or manually execute SQL queries.

2. **Update the `wp-config.php` File:**
   - Ensure you've updated the database name, username, and password in the `wp-config.php` file.
   - Verify the `WP_HOME` and `WP_SITEURL` constants in `wp-config.php` if you've added them.
     ```php
     define('WP_HOME','http://your-new-domain.com');
     define('WP_SITEURL','http://your-new-domain.com');
     ```

3. **Permalinks:**
   - Go to `Settings -> Permalinks` in the WordPress dashboard and simply click "Save Changes." This often refreshes the permalink structure and can fix 404 errors.

4. **Check .htaccess File: ( if apache is used )**
   - Ensure the `.htaccess` file is correctly set up. You can regenerate it by saving the permalinks as mentioned above or manually add the following for standard WordPress setups:
     ```plaintext
     # BEGIN WordPress
     <IfModule mod_rewrite.c>
     RewriteEngine On
     RewriteBase /
     RewriteRule ^index\.php$ - [L]
     RewriteCond %{REQUEST_FILENAME} !-f
     RewriteCond %{REQUEST_FILENAME} !-d
     RewriteRule . /index.php [L]
     </IfModule>
     # END WordPress
     ```

5. **File Permissions:**
   - Check that your file and folder permissions are correct. Generally, directories should be `755` and files should be `644`.

6. **Clear Cache:**
   - If you're using any caching plugins, clear the cache. Also, clear your browser cache or try accessing the site in incognito mode.

7. **Check for Mixed Content Issues:**
   - If your site is HTTPS and some elements are still HTTP, it may cause issues. Use a plugin like "Really Simple SSL" to fix these.

8. **Update DNS Settings:**
   - Ensure that the domain's DNS settings are correctly pointed to the new server.

9. **Check for Hardcoded URLs in Theme or Plugins:**
   - Some themes or plugins might have hardcoded URLs that need updating.

10. **Error Logs:**
    - Check the server’s error logs for any clues as to what might be going wrong.

If after all these steps your website is still not functioning correctly, could you provide more specific details about the issue? For example, are you seeing a specific error message, or is the site simply not loading? This can help narrow down the problem.