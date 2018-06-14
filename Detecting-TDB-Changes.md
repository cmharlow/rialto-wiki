Jena provides a ModelChangedListener Java interface that we could use to build our own listener/event notification mechanism:

https://jena.apache.org/documentation/notes/event-handler-howto.html

https://jena.apache.org/documentation/javadoc/jena/org/apache/jena/rdf/model/ModelChangedListener.html

The source code for our two Java TDB loading classes are here:

https://github.com/sul-dlss-labs/Vitro/blob/73-tdb-load/rialto/src/main/java/edu/stanford/RialtoLoad.java

https://github.com/sul-dlss-labs/Vitro/blob/73-tdb-load/rialto/src/main/java/RialtoArq.java

I suspect that the method used in RialtoLoad would definitely work, while I am a little less certain about the RialtoArq method (that uses Dataset instead of Model for the update).