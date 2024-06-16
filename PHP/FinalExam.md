- 8307
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>String Replace in PHP</title>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>String Replace in PHP</title>
</head>
<body>
    <h1>PHP 字串替換工具</h1>
    <form method="post">
        <label for="subject">原始字串：</label>
        <input type="text" id="subject" name="subjecttxt" required><br><br>  		
        <label for="search">查找字串：</label>
        <input type="text" id="search" name="searchtxt" required><br><br>
        <label for="replace">替換成：</label>
        <input type="text" id="replace" name="replacetxt" required><br><br>
        <button type="submit" name="submit">替換字串</button>
    </form> 
    <?php
        if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST['submit'])) {
            // 確保所有表單元素都已設定. 使用 isset() 函數來檢查這些鍵是否存在於 $_POST 數組中
            if (isset($_POST['searchtxt']) && isset($_POST['replacetxt']) && isset($_POST['subjecttxt'])) {
                // 獲取表單資料
                $search_s = $_POST['searchtxt'];
                $replace_s = $_POST['replacetxt'];
                $subject_s = $_POST['subjecttxt'];

                // 執行字串替換
                $replacedText = str_replace($search_s, $replace_s, $subject_s);

                // 顯示結果
                //echo "<p>原始字串: " . htmlspecialchars($subject_s) . "</p>";
                //echo "<p>被取代的字串是: " . htmlspecialchars($replacedText) . "</p>";
				echo "<p>原始字串: " . $subject_s . "</p>";
                echo "<p>被取代的字串是: " . $replacedText . "</p>";
            } else {
                echo "<p>請填寫所有欄位。</p>";
            }
        }
    ?>
</body>
</html>
```
- 8311a
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSV 文件上傳與顯示</title>
    <style>
        table {
            border-collapse: collapse;
            width: 100%;
        }
        th {
            background-color: blue;
            color: white;
            padding: 8px;
            text-align: left;
        }
        td {
            padding: 8px;
            text-align: left;
        }
    </style>
</head>
<body>
    <h1>上傳並顯示 CSV 文件內容</h1>
    <form action="" method="post" enctype="multipart/form-data">
        <label for="file">選擇 CSV 文件:</label>
        <input type="file" id="file" name="file" accept=".csv" required><br><br>
        <button type="submit" name="submit">上傳並顯示</button>
    </form>

    <?php
    if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_FILES["file"]) && isset($_POST["submit"])) {
        $file = $_FILES["file"];
        // 檢查文件是否上傳成功
        if ($file["error"] != UPLOAD_ERR_OK) {
            echo "<p>文件上傳失敗。</p>";
            exit;
        }
        // 確保上傳的是一個 CSV 文件
        $fileType = pathinfo($file["name"], PATHINFO_EXTENSION);
        if ($fileType != "csv") {
            echo "<p>請上傳一個 CSV 文件。</p>";
            exit;
        }
        // 讀取 CSV 文件內容
        $filePath = $file["tmp_name"];
        if (($handle = fopen($filePath, "r")) !== false) {
            echo "<h2>文件內容:</h2>";
            echo "<table>";
            // 讀取 CSV 文件的標頭
            if (($header = fgetcsv($handle, 1000, ",")) !== false) {
                echo "<tr>";
                foreach ($header as $col) {
                    echo "<th>" . htmlspecialchars($col) . "</th>";
                }
                echo "</tr>";
            }
            // 讀取 CSV 文件的每一行數據
            while (($data = fgetcsv($handle, 1000, ",")) !== false) {
                echo "<tr>";
                foreach ($data as $col) {
                    echo "<td>" . htmlspecialchars($col) . "</td>";
                }
                echo "</tr>";
            }
            echo "</table>";
            fclose($handle);
        } else {
            echo "<p>讀取文件有誤。</p>";
        }
    } else {
        echo "<p>等待輸入!</p>";
    }
    ?>
</body>
</html>

```
- 8311b
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSV 文件上傳與顯示</title>
    <style>
        table {
            border-collapse: collapse;
            width: 100%;
        }
        th {
            background-color: blue;
            color: white;
            padding: 8px;
            text-align: left;
        }
        td {
            padding: 8px;
            text-align: left;
        }
    </style>
</head>
<body>
    <h1>上傳並顯示 CSV 文件內容</h1>
    <form action="" method="post" enctype="multipart/form-data">
        <label for="file">選擇 CSV 文件:</label>
        <input type="file" id="file" name="file" accept=".csv" required><br><br>
        <button type="submit" name="submit">上傳並顯示</button>
    </form>

    <?php
    if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_FILES["file"]) && isset($_POST["submit"])) {
        $file = $_FILES["file"];
        // 檢查文件是否上傳成功
        if ($file["error"] != UPLOAD_ERR_OK) {
            echo "<p>文件上傳失敗。</p>";
            exit;
        }
        // 確保上傳的是一個 CSV 文件
        $fileType = pathinfo($file["name"], PATHINFO_EXTENSION);
        if ($fileType != "csv") {
            echo "<p>請上傳一個 CSV 文件。</p>";
            exit;
        }
        // 讀取 CSV 文件內容
        $filePath = $file["tmp_name"];
        if (($handle = fopen($filePath, "r")) !== false) {
            echo "<h2>文件內容:</h2>";
            echo "<table>";
            // 讀取 CSV 文件的標頭
            if (($header = fgetcsv($handle, 1000, ",")) !== false) {
                echo "<tr>";
                foreach ($header as $col) {
                    echo "<th>" . htmlspecialchars($col) . "</th>";
                }
                echo "<th>備註</th>";
                echo "</tr>";
            }
            // 讀取 CSV 文件的每一行數據
            while (($data = fgetcsv($handle, 1000, ",")) !== false) {
                echo "<tr>";
                foreach ($data as $index => $col) {
                    echo "<td>" . htmlspecialchars($col) . "</td>";
                }
                $grade = (int) $data[count($data) - 1]; // 假設成績在最後一列
                $remark = $grade < 60 ? "不及格" : "";
                echo "<td>" . htmlspecialchars($remark) . "</td>";
                echo "</tr>";
            }
            echo "</table>";
            fclose($handle);
        } else {
            echo "<p>讀取文件有誤。</p>";
        }
    } else {
        echo "<p>等待輸入!</p>";
    }
    ?>
</body>
</html>
```
- 8312
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSV 文件上傳與顯示</title>
</head>
<body>
    <h1>上傳並顯示 CSV 文件內容</h1>
    <form action="" method="post" enctype="multipart/form-data">
        <label for="file">選擇 CSV 文件:</label>
        <input type="file" id="file" name="file" accept=".csv" required><br><br>
        <button type="submit" name="submit">上傳並顯示</button>
    </form>

    <div id="content">
        <?php
        if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST["submit"]) && isset($_FILES["file"])) {
            $file = $_FILES["file"];
            // 檢查文件是否上傳成功
            if ($file["error"] != UPLOAD_ERR_OK) {
                echo "<p>文件上傳失敗。</p>";
                exit;
            }
            // 確保上傳的是一個 CSV 文件
            $fileType = pathinfo($file["name"], PATHINFO_EXTENSION);
            if ($fileType != "csv") {
                echo "<p>請上傳一個 CSV 文件。</p>";
                exit;
            }

            // 讀取 CSV 文件內容
            $filePath = $file["tmp_name"];
            if (($handle = fopen($filePath, "r")) !== false) {
                // 連接到資料庫
                $servername = "localhost"; // 資料庫伺服器名稱
                $username = "root"; // 資料庫用戶名
                $password = ""; // 資料庫密碼
                $dbname = "ksu_database"; // 資料庫名稱

                // 創建連接
                $conn = new mysqli($servername, $username, $password, $dbname);

                // 檢查連接
                if ($conn->connect_error) {
                    die("<p>資料庫連接失敗: " . $conn->connect_error . "</p>");
                }

                echo "<h2>顯示文件內容, 並寫入資料庫:</h2>";
                echo "<table border='1'>";

                // 讀取 CSV 文件的標頭
                if (($header = fgetcsv($handle, 1000, ",")) !== false) {
                    echo "<tr>";
                    foreach ($header as $col) {
                        echo "<th>" . htmlspecialchars($col) . "</th>";
                    }
                    echo "</tr>";
                }

                // 讀取 CSV 文件的每一行數據
                while (($data = fgetcsv($handle, 1000, ",")) !== false) {
                    echo "<tr>";
                    foreach ($data as $col) {
                        echo "<td>" . htmlspecialchars($col) . "</td>";
                    }
                    echo "</tr>";

                    // 準備並執行插入資料庫的 SQL 語句
                    $departmentID = $conn->real_escape_string($data[0]);
                    $studentID = $conn->real_escape_string($data[1]);
                    $studentName = $conn->real_escape_string($data[2]);
                    $sex = $conn->real_escape_string($data[3]);
                    $grade = $conn->real_escape_string($data[4]);

                    $sql = "INSERT INTO student_grade (t_departmentID, t_studentID, t_studentName, t_sex, t_grade) VALUES ('$departmentID', '$studentID', '$studentName', '$sex', '$grade')";
                    if (!$conn->query($sql)) {
                        echo "<p>插入資料庫失敗: " . $conn->error . "</p>";
                    }
                }
                echo "</table>";
                fclose($handle);

                // 關閉資料庫連接
                $conn->close();
            } else {
                echo "<p>讀取文件有誤。</p>";
            }
        } else {
            echo "<p>等待輸入!</p>";
        }
        ?>
    </div>
</body>
</html>

```
-8312a
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSV 文件上傳與顯示</title>
</head>
<body>
    <h1>上傳並顯示 CSV 文件內容</h1>
    <form action="" method="post" enctype="multipart/form-data">
        <label for="file">選擇 CSV 文件:</label>
        <input type="file" id="file" name="file" accept=".csv" required><br><br>
        <button type="submit" name="submit">上傳並顯示</button>
    </form>

    <div id="content">
        <?php
        if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST["submit"]) && isset($_FILES["file"])) {
            $file = $_FILES["file"];
            // 檢查文件是否上傳成功
            if ($file["error"] != UPLOAD_ERR_OK) {
                echo "<p>文件上傳失敗。</p>";
                exit;
            }
            // 確保上傳的是一個 CSV 文件
            $fileType = pathinfo($file["name"], PATHINFO_EXTENSION);
            if ($fileType != "csv") {
                echo "<p>請上傳一個 CSV 文件。</p>";
                exit;
            }

            // 讀取 CSV 文件內容
            $filePath = $file["tmp_name"];
            if (($handle = fopen($filePath, "r")) !== false) {
                // 連接到資料庫
                $servername = "localhost"; // 資料庫伺服器名稱
                $username = "root"; // 資料庫用戶名
                $password = ""; // 資料庫密碼
                $dbname = "ksu_database"; // 資料庫名稱

                // 創建連接
                $conn = new mysqli($servername, $username, $password, $dbname);

                // 檢查連接
                if ($conn->connect_error) {
                    die("<p>資料庫連接失敗: " . $conn->connect_error . "</p>");
                }

                // 檢查並創建資料表
                $checkTableSql = "CREATE TABLE IF NOT EXISTS student_grade (
                    t_departmentID VARCHAR(10),
                    t_studentID VARCHAR(10),
                    t_studentName VARCHAR(50),
                    t_sex VARCHAR(10),
                    t_grade INT
                );";
                if (!$conn->query($checkTableSql)) {
                    die("<p>創建資料表失敗: " . $conn->error . "</p>");
                }

                echo "<h2>顯示文件內容, 並險入資料庫:</h2>";
                echo "<table border='1'>";

                // 讀取 CSV 文件的標頭
                if (($header = fgetcsv($handle, 1000, ",")) !== false) {
                    echo "<tr>";
                    foreach ($header as $col) {
                        echo "<th>" . htmlspecialchars($col) . "</th>";
                    }
                    echo "</tr>";
                }

                // 讀取 CSV 文件的每一行數據
                while (($data = fgetcsv($handle, 1000, ",")) !== false) {
                    echo "<tr>";
                    foreach ($data as $col) {
                        echo "<td>" . htmlspecialchars($col) . "</td>";
                    }
                    echo "</tr>";

                    // 準備並執行插入資料庫的 SQL 語句
                    $departmentID = $conn->real_escape_string($data[0]);
                    $studentID = $conn->real_escape_string($data[1]);
                    $studentName = $conn->real_escape_string($data[2]);
                    $sex = $conn->real_escape_string($data[3]);
                    $grade = $conn->real_escape_string($data[4]);

                    $sql = "INSERT INTO student_grade (t_departmentID, t_studentID, t_studentName, t_sex, t_grade) VALUES ('$departmentID', '$studentID', '$studentName', '$sex', '$grade')";
                    if (!$conn->query($sql)) {
                        echo "<p>插入資料庫失敗: " . $conn->error . "</p>";
                    }
                }
                echo "</table>";
                fclose($handle);

                // 關閉資料庫連接
                $conn->close();
            } else {
                echo "<p>讀取文件有誤。</p>";
            }
        } else {
            echo "<p>等待輸入!</p>";
        }
        ?>
    </div>
</body>
</html>

```
