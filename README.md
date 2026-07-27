# kryo-jdkgdxds
Kryo 5.x support for classes from [jdkgdxds](https://github.com/tommyettinger/jdkgdxds)

## Get it

Use JitPack.io as your repository (which gdx-liftoff projects already can do) and depend on:
```
implementation "com.github.tommyettinger:kryo-jdkgdxds:2.1.6.2"
```

This release is compatible with jdkgdxds 2.1.6 and Kryo 5.6.2 .

## Usage

Register the jdkgdxds types using their appropriate serializers from this library. You can look at the tests here
for how they do this, or just see the source for ObjectDeque's serialization test here:

```java
    @Test
    public void testObjectDeque() {
        Kryo kryo = new Kryo();
        kryo.register(ObjectDeque.class, new ObjectDequeSerializer());

        ObjectDeque<String> data = ObjectDeque.with("-123.123", "0", "Four-Fifty Six", "0", "1.0", "-1.0", "0.000001");

        Output output = new Output(32, -1);
        kryo.writeObject(output, data);
        byte[] bytes = output.toBytes();
        try (Input input = new Input(bytes)) {
            ObjectDeque data2 = kryo.readObject(input, ObjectDeque.class);
            Assert.assertEquals(data, data2);
        }
    }
```

This tests:

- Registering ObjectDeque with Kryo so it uses ObjectDequeSerializer,
- Writing an ObjectDeque to a Kryo Output, and
- Reading a copy of the original ObjectDeque back, asserting the two are equivalent.

## Older Versions

See [kryo-more](https://github.com/tommyettinger/kryo-more) for older releases.

## License

[Apache 2.0](LICENSE).