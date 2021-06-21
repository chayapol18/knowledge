# PHP

## Syntax
    <?php
    // PHP code goes here
    ?>

    - The default file extension for PHP files is ".php".
    - PHP statements end with a semicolon (;).

    <?php
    echo "Hello World!";
    ?>
    build-in function "echo" ไว้สำหรับแสดงค่าหรือตัวแปรที่เรากำหนดบนหน้าเว็บ

## Comment
    - single line
      use // comment, # comment
    - multiple line
      use /* */

## Variable
    - $ + variableName
      ex.
        <?php
        $txt = "Hello world!";
        $x = 5;
        $y = 10.5;
        ?>
    - A variable can have a short name (like x and y) or a more descriptive name (age, carname, total_volume).
    - ขึ้นต้นด้วยตัวเลข ไม่ได้ต้องขึ้นต้นด้วยตัวอักษรไม่ก็ underscore
    - ตัวเล็กตัวใหญ่ถือว่าเป็นคนละตัวแปร

    How to use variable
    ex. 
      <?php
      $txt = "W3Schools.com";
      echo "I love $txt!";
      ?>

      <?php
      $txt = "W3Schools.com";
      echo "I love " . $txt . "!";
      ?>

      output of both: "I love W3Schools.com"

      <?php
      $x = 5;
      $y = 4;
      echo $x + $y;
      ?>

      output: 9

    Variables scope
    <?php
    $x = 5; // global scope

    function myTest() {
      // using x inside this function will generate an error
      echo "<p>Variable x inside function is: $x</p>";
    }
    myTest();

    echo "<p>Variable x outside function is: $x</p>";
    ?>

    - จากตัวอย่างจะเห็นว่าไม่สามารถใช้ตัวแปรที่เป็น global ใน function ได้
    และจะไม่สามารถใช้ตัวแปรใน function นั้นข้างนอกได้เช่นกัน

    - ถ้าจะเอาตัวแปร global ไปใช้ใน function ต้องประกาศตามตัวอย่างนี้
    ex. 
      <?php
      $x = 5;
      $y = 10;

      function myTest() {
        global $x, $y; //เอาตัวแปร global มาใช้
        $y = $x + $y;
      }

      myTest();
      echo $y; // outputs 15
      ?>

    - หรือถ้าต้องการ overwrite ค่าของตัวแปร global ให้ทำวิธีดังนี้
    ex.
      <?php
      $x = 5;
      $y = 10;

      function myTest() {
        $GLOBALS['y'] = $GLOBALS['x'] + $GLOBALS['y'];
      }

      myTest();
      echo $y; // outputs 15
      ?>