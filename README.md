# Logstash output for Apache Pulsar

## Developing

### 1. Plugin Developement and Testing

#### Code
- Install dependencies

```sh
bundle install
```
- Update your dependencies

```sh
bundle update
```

## Test

On jruby:
- Run unit tests
```bash
bundle exec rake vendor
```
- Run integration tests
```sh
bundle exec rspec
```

## Informations

```bash
jruby -S <command>
```

### 2. Running your unpublished Plugin in Logstash

#### 2.1 Run in a local Logstash clone

- Edit Logstash `Gemfile` and add the local plugin path, for example:
```ruby
gem "logstash-output-pulsar", :path => "/your/local/logstash-output-pulsar"
```
- Install plugin
```sh
# Logstash 2.3 and higher
bin/logstash-plugin install --no-verify

# Prior to Logstash 2.3
bin/plugin install --no-verify

```
- Run Logstash with your plugin
```sh
bin/logstash -e 'output { pulsar { topic_id => "pulsar_topic" }}'
```
At this point any modifications to the plugin code will be applied to this local Logstash setup. After modifying the plugin, simply rerun Logstash.

#### 2.2 Run in an installed Logstash

You can use the same **2.1** method to run your plugin in an installed Logstash by editing its `Gemfile` and pointing the `:path` to your local plugin development directory or you can build the gem and install it using:

- Build your plugin gem
```sh
gem build logstash-output-pulsar.gemspec
```
- Install the plugin from the Logstash home with "--local" option
```sh
bin/plugin install --local /usr/share/plugins/logstash-output-pulsar/logstash-output-pulsar-1.0.0.gem 
```
- You can find installed plugin
```sh
find ./ -name logstash-output-pulsar*
./vendor/local_gems/4280b97c/logstash-output-pulsar-1.1.0.pre.SNAPSHOT
./vendor/local_gems/4280b97c/logstash-output-pulsar-1.1.0.pre.SNAPSHOT/logstash-output-pulsar.gemspec
./vendor/local_gems/4280b97c/logstash-output-pulsar-1.1.0.pre.SNAPSHOT/lib/logstash-output-pulsar_jars.rb
./vendor/cache/logstash-output-pulsar-1.1.0.pre.SNAPSHOT.gem
```
- Start Logstash and proceed to test the plugin
