# JDK-8282446
https://bugs.openjdk.java.net/browse/JDK-8282446

```java
public sealed interface Foo {
    record Bar() implements Foo {}
}
```

- `javac -d out Foo.java`
- `jar --create --file foo.jar -C out .`
- `jar --validate --file foo.jar`

```text
java.lang.UnsupportedOperationException: This feature requires ASM9_EXPERIMENTAL
	at java.base/jdk.internal.org.objectweb.asm.ClassVisitor.visitPermittedSubclassExperimental(ClassVisitor.java:299)
	at java.base/jdk.internal.org.objectweb.asm.ClassReader.accept(ClassReader.java:715)
	at java.base/jdk.internal.org.objectweb.asm.ClassReader.accept(ClassReader.java:432)
	at jdk.jartool/sun.tools.jar.FingerPrint.getClassAttributes(FingerPrint.java:165)
	at jdk.jartool/sun.tools.jar.FingerPrint.<init>(FingerPrint.java:81)
	at jdk.jartool/sun.tools.jar.Validator.getFingerPrint(Validator.java:142)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.stream.ReferencePipeline$2$1.accept(ReferencePipeline.java:179)
	at java.base/java.util.zip.ZipFile$EntrySpliterator.tryAdvance(ZipFile.java:558)
	at java.base/java.util.Spliterator.forEachRemaining(Spliterator.java:332)
	at java.base/java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:509)
	at java.base/java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:499)
	at java.base/java.util.stream.ReduceOps$ReduceOp.evaluateSequential(ReduceOps.java:921)
	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:234)
	at java.base/java.util.stream.ReferencePipeline.collect(ReferencePipeline.java:682)
	at jdk.jartool/sun.tools.jar.Validator.validate(Validator.java:83)
	at jdk.jartool/sun.tools.jar.Validator.validate(Validator.java:74)
	at jdk.jartool/sun.tools.jar.Main.validateJar(Main.java:436)
	at jdk.jartool/sun.tools.jar.Main.run(Main.java:414)
	at jdk.jartool/sun.tools.jar.Main.main(Main.java:1665)
```
