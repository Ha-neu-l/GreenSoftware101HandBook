# <span style="color: #00BF63; font-family:Monaco, monospace">Examples of Codes </span>

<img src="assets/samples/4_Code.png" alt="Practices" style="width:100%;height:300px;">

> “As software continues to demonstrate its contribution to unprecedented levels of greenhouse gas emissions, green coding will become more > and more imperative to make our habitual use of technology more sustainable – as the world isn’t going to stop using software or technology altogether.” <br>

Below are examples of common energy-consuming code practices and their more sustainable, greener alternatives. All examples are provided in PHP and they are just for showing an idea:


* #### <span style="color: #84ffc4;"> Example 1: _Efficient Database Querying_</span> <br>
    * **Unsustainable Case**:

        ```php
        <?php
            // Fetching all records and then filtering in PHP
            $results = $db->query("SELECT * FROM users");
            $activeUsers = [];
            while ($row = $results->fetch_assoc()) {
                if ($row['status'] == 'active') {
                $activeUsers[] = $row;
                }
            }
        ?>
        ```
    * **Green way**:

        ```php
        <?php
            $activeUsers = $db->query("SELECT id FROM users WHERE status = 'active'");
        ?>
        ```
-> By filtering records directly in the SQL query &, the database server does less work, and less data is transferred to the application, reducing both processing power and energy consumption. Also specifying the columns needed is very important part of optimizing a query.

<br>

* #### <span style="color: #84ffc4;">Example 2: _Efficient Use of Loops and Functions_</span> <br>
    * **Unsustainable Case**:

        ```php
        <?php
            // Inefficient loop with repeated function calls for
            for ($i = 0; $i < strlen($string); $i++) { echo $string[$i]; }

        ?>
        ```
    * **Green way**:

        ```php
        <?php
            // Calculating string length once outside the loop
            $length = strlen($string);
            for ($i = 0; $i < $length; $i++) { echo $string[$i]; }

        ?>
        ```
-> Calculating the string length inside the loop calls the function multiple times. Calculating it once outside the loop reduces CPU cycles, leading to less energy usage.

<br>

* #### <span style="color: #84ffc4;">Example 3: _Using Array Functions Efficiently_</span> <br>
    * **Unsustainable Case**:

        ```php
        <?php
            // Filtering an array using a loop
            $filtered = [];
            foreach ($array as $item) {
                if ($item['value'] > 10) {
                    $filtered[] = $item;
                }
            }

        ?>
        ```
    * **Green way**:

        ```php
        <?php
            // Using array_filter for efficient & faster filtering
            $filtered = array_filter($array, function($item) { return $item['value'] > 10; });

        ?>
        ```
-> Using built-in array functions like array_filter is more efficient than manually looping through arrays. These functions are optimized in PHP's core, reducing CPU cycles and energy usage.

<br>

* #### <span style="color: #84ffc4;">Example 4: _Minimizing Database Calls_</span> <br>
    * **Unsustainable Case**:

        ```php
        <?php
            // Making multiple database calls in a loop
            $userIds = [1, 2, 3];
            foreach ($userIds as $userId) {
                $stmt = $pdo->prepare("SELECT * FROM users WHERE id = :id"); $stmt->execute([':id' => $userId]);
                $user = $stmt->fetch(PDO::FETCH_ASSOC); echo $user['username'] . '<br>'; 
            }

        ?>
        ```
    * **Green way**:

        ```php
        <?php
            // Using a single query with an IN clause to fetch multiple rows
            $userIds = [1, 2, 3];
            $placeholders = implode(',', array_fill(0, count($userIds), '?'));
            $stmt = $pdo->prepare("SELECT * FROM users WHERE id IN ($placeholders)");$stmt->execute($userIds);
            $users = $stmt->fetchAll(PDO::FETCH_ASSOC);
            foreach ($users as $user) { 
                echo $user['username'] . '<br>'; 
            }

        ?>
        ```
-> Reducing the number of database calls minimizes server-side processing and network overhead, leading to lower energy consumption and improved application performance.


> “Think about sustainability before going into the solution—and not after.”

<br><br>
⬅️ [**Best Practices For a Greener Software Development**](3_best_practices_for_a_green_software_dev.md)
<br>
➡️ [**Technologies & Tools**](5_technologies_&_tools.md)