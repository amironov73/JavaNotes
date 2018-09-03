### Ввод-вывод

Общего предка для всех потоков ввода-вывода в Java нет. Есть `InputStream` и отдельно `OutputStream`.

#### InputStream

* **int available()** - число байтов, доступных для чтения.

* **void close()** - закрывает поток.

* **int read()** - возвращает следующий байт в потоке (в виде `int`) или отрицательное число, если достигнут конец потока.

* **int read(byte[] buffer)** - считывает байты из потока в буфер. Возвращает число прочитанных байтов либо отрицательное число. 

* **int read(byte[] buffer, int offset, int length)** - аналогично предыдущему методу.

* **long skip(long number)** - пропускает в потоке некоторое количество байт. Возвращает число успешно пропущенных байт.

#### OutputStream

* **void close()** - закрывает поток.

* **void flush()** - "выталкивает" данные из кэша (если они там есть) на диск, в сеть и т. д.

* **void write(int b)** - записывает в поток один байт.

* **void write(byte[] buffer)** - записывает в поток массив байтов.

* **void write(byte[] buffer, int offset, int length)** - записывает в поток массив байтов.

#### Reader

* **void close()** - закрывает поток.

* **int read()** - возвращает следующий символ в потоке (в виде `int`) либо отрицательное число, если достигнут конец.

* **int read(char[] buffer)** - считывает символы из потока. Возвращает число успешно считанных символов, либо отрицательное число, если достигнут конец.

* **int read(CharBuffer buffer)** - аналогично предыдущему.

* **int read(char[] buffer, int offset, int count)** - аналогично предыдущему.

* **long skip(long count)** - пропускает указанное количество символов. Возвращает число успешно пропущенных символов.

#### Writer

* **Writer append(char c)** - добавляет символ в конец выходного потока.

* **Writer append(CharSequence chars)** - добавляет в конец выходного потока последовательность символов.

* **void close()** - закрывает поток.

* **void flush()** - "выталкивает" хранящиеся в кэше символы (если они там есть) на диск, в сеть и т. д.

* **void write(int c)** - записывает в поток один символ.

* **void write(char[] buffer)** - записывает в поток массив символов.

* **void write(char[] buffer, int off, int len)** - записывает в поток только несколько символов из массива.

* **void write(String str)** - записывает в поток строку.

* **void write(String str, int off, int len)** - записывает в поток несколько символов из строки.

#### FileOutputStream

Конструкторы:

```java
FileOutputStream(String filePath);
FileOutputStream(File fileObj);
FileOutputStream(String filePath, boolean append);
FileOutputStream(File fileObj, boolean append);
```

Пример использования:

```java
import java.io.FileOutputStream;
import java.io.IOException;
 
public class Program {
  
    public static void main(String[] args) {
          
        String text = "Hello world!";
        try(FileOutputStream fos=new FileOutputStream("C:/SomeDir/notes.txt")) {
            byte[] buffer = text.getBytes();              
            fos.write(buffer, 0, buffer.length);
        }
        catch(IOException ex) {
            ex.printStackTrace();
        }
        System.out.println("Success");
    }
}
```

### FileInputStream

```java
import java.io.FileInputStream;
import java.io.IOException;
 
public class Program {
  
    public static void main(String[] args) {
 
        try(FileInputStream fin=new FileInputStream("C:/SomeDir/notes.txt")) {
            byte[] buffer = new byte[fin.available()];
            fin.read(buffer, 0, buffer.length);
            String text = new String(buffer);
            System.out.println(text);
        }
        catch(IOException ex) {
            ex.printStackTrace();
        } 
    }
}
```
