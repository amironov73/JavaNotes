### Работа с кодировками

Самый управляемый сценарий преобразования строки в байты:

```java
import java.nio.ByteBuffer;
import java.nio.CharBuffer;
import java.nio.charset.CharacterCodingException;
import java.nio.charset.Charset;
import java.nio.charset.CharsetEncoder;
import java.nio.charset.CodingErrorAction;
import java.util.Arrays;

class Scratch {
    public static void main(String[] args) {
        Charset charset = Charset.forName("cp1251");
        CharsetEncoder encoder = charset.newEncoder()
                .onMalformedInput(CodingErrorAction.REPLACE)
                .onUnmappableCharacter(CodingErrorAction.REPLACE);
        String text = "У попа была собака";
        ByteBuffer buffer = null;
        try {
            buffer = encoder.encode(CharBuffer.wrap(text));
        } catch (CharacterCodingException e) {
            e.printStackTrace();
        }
        byte[] result = null;
        if (buffer != null) {
            result = buffer.array();
            if (buffer.limit() != result.length) {
                result = Arrays.copyOf(result, buffer.limit());
            }
        }
        if (result != null) {
            System.out.println(Arrays.toString(result));
        }
    }
}
```

Самый простой сценарий:

```java
import java.nio.charset.Charset;
import java.util.Arrays;

class Scratch {
    public static void main(String[] args) {
        Charset charset = Charset.forName("cp1251");
        String text = "У попа была собака";
        byte[] result = text.getBytes(charset);
        System.out.println(Arrays.toString(result));
    }
}
```

Получение длины строки в указанной кодировке:

```java
import java.nio.charset.Charset;

class Scratch {
    static int getByteCount(String text, Charset encoding) {
        return text.getBytes(encoding).length;
    }

    public static void main(String[] args) {
        Charset charset = Charset.forName("cp1251");
        String text = "У попа была собака";
        int result = getByteCount(text, charset);
        System.out.println(result);
    }
}
```

