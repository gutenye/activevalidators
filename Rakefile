require 'rubygems'
require 'rubygems/specification'

require 'bundler'
Bundler::GemHelper.install_tasks

require 'rake/testtask'
Rake::TestTask.new do |t|
  t.libs << "test"
  t.pattern = "test/**/*_test.rb"
  t.verbose = true
  t.warning = true
end

require 'turn'

# -*- encoding: utf-8 -*-
$:.unshift File.expand_path("../lib", __FILE__)
require 'activevalidators'

def gemspec
  @gemspec ||= begin
                 file = File.expand_path('../activevalidators.gemspec', __FILE__)
                 eval(File.read(file), binding, file)
               end
end

desc "Clean the current directory"
task :clean do
  rm_rf 'tmp'
  rm_rf 'pkg'
end

desc "Run the full spec suite"
task :full => ["clean", "test"]

desc "install the gem locally"
task :install => :package do
  sh %{gem install pkg/#{gemspec.name}-#{gemspec.version}}
end

desc "validate the gemspec"
task :gemspec do
  gemspec.validate
end

desc "Build the gem"
task :gem => [:gemspec, :build] do
  mkdir_p "pkg"
  sh "gem build activevalidators.gemspec"
  mv "#{gemspec.full_name}.gem", "pkg"
end

desc "Install ActiveValidators"
task :install => :gem do
  sh "gem install pkg/#{gemspec.full_name}.gem"
end

task :default => :full
