
## JENKINS_PARTITIONS rake test:jenkins:partition:4 
require 'socket'


namespace :test do
  namespace :jenkins do
    namespace :partition do 

      desc "run the selected partition, see test:jenkins:partition:p#"
      task :run do 
          pretend_tests   = 100.times.map{ |i| "test_#{i}" }
          partitions      = ENV['JENKINS_PARTITIONS'  ].to_i
          partition_id    = ENV['JENKINS_PARTITION_ID'].to_i
          partition_size  = pretend_tests.size / partitions

          partition_start = partition_id    * partition_size
          partition_stop  = partition_start + partition_size
          selected_tests  = pretend_tests[partition_start...partition_stop]

          prefix = "#{Socket.gethostname}/p#{partition_id}"
          puts "#{prefix}: id=#{partition_id} size=#{partition_size}|#{selected_tests.size} count=#{partitions}"
          selected_tests.each do |test|
            puts "#{prefix}: #{test}"          
          end
          puts "#{prefix}: Now that you're here, I'm going to sleep for a bit... to look busy!" 
          sleep 15
          puts "#{prefix}: Done" 
      end

      5.times.each do |partition|
        desc "run partition p#{partition}"
        task "p#{partition}".to_sym do 
          ENV['JENKINS_PARTITION_ID'] = partition.to_s
          Rake::Task['test:jenkins:partition:run'].invoke
        end
      end
    end


  end
end
