# Database setup (XAMPP + MySQL)

The app now saves everything (accounts, modules and stocks, appointments, notifications, queries, feedback,
activity log) in a MySQL database. Passwords are stored as salted PBKDF2 hashes.

## One-time setup
1. Open the **XAMPP Control Panel** and **Start** the **MySQL** module (Apache is not needed by the app;
   start it only if you want phpMyAdmin at http://localhost/phpmyadmin).
2. Download **MySQL Connector/J** (Platform Independent ZIP) from https://dev.mysql.com/downloads/connector/j/
   and copy the `.jar` inside it into the project's **`lib`** folder.
3. Check `db.properties` (project folder). The defaults fit a fresh XAMPP: user `root`, empty password,
   database `module_distribution`.
4. Run the project. On first start the app creates the database and tables and adds the sample data
   (same demo logins as before: edmund@example.edu / student123, mark.sanchez@staff.edu / staff123,
   admin@smms.edu / admin123). From then on it loads and saves your real data.

If the database can't be reached, the app still opens with in-memory sample data and shows a warning
("Running without a database"); nothing is saved in that mode.

## Notes
- Table layout: `src/moduledistributionsystem/resources/schema.sql` (run automatically; you can also import it in phpMyAdmin).
- Several computers can share one database: point `db.host` at the computer running XAMPP (allow that user
  in MySQL). Screens re-read the database whenever you switch sections and at login.
- Removing a module hides it from the inventory but keeps its row, so old appointments still show it.
- Stock changes from pickups are done in SQL (`stocks = stocks + ?`), so two computers can't overwrite each other's count.
- Change the default `root` password and the demo passwords before real use.
