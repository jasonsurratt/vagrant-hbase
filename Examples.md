= Examples

Here are a few examples to get you started with JanusGraph

== Greek God Data with Cassandra and ElasticSearch

  # gain access to the VM from the host
  vagrant ssh

  # Start the server
  janusgraph/bin/janusgraph.sh

  # Start the JanusGraph client
  janusgraph/bin/bin/gremlin.sh


  # Connect to the JanusGraph server
  :remote connect tinkerpop.server conf/remote.yaml
  # if you haven't loaded the graph already
  :> GraphOfTheGodsFactory.load(graph)

  # Print out the vertices within three hops of hercules
  :> g = graph.traversal()
  :> g.V().has('name', 'hercules').repeat(out()).times(3).tree().by('name')


== Greek God Data with HBase and ElasticSearch

This runs in process and makes calls to hbase.

  # gain access to the VM from the host
  vagrant ssh

  # Start the JanusGraph client
  janusgraph/bin/bin/gremlin.sh

  # Start an in-process JanusGraph server that talks to HBase and runs elasticsearch in process as well.
  graph = JanusGraphFactory.open('conf/janusgraph-hbase-es-vagrant.properties')
  # if you haven't loaded the graph already
  GraphOfTheGodsFactory.load(graph)

  # Print out the vertices within three hops of hercules
  g = graph.traversal()
  g.V().has('name', 'hercules').repeat(out()).times(3).tree().by('name')
