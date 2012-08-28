require 'bundler'
require "rake/clean"
require "fileutils"
require 'rake/testtask'

Bundler::GemHelper.install_tasks

task :default => :test
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/*_test.rb'
  test.verbose = true
end


namespace :production do

  CLOBBER.include('output')

  desc "Run unit specs"
  task :unit do
    sh "rspec spec/unit/"
  end

  desc "Run functional specs"
  task :func => [:clobber] do
    FileUtils.cd "platform_descriptor/e4/"
    sh "ruby ../../bin/fc_config e4.rb"

    FileUtils.cd "../e5"
    sh "ruby ../../bin/fc_config e5.rb"

    FileUtils.cd "../.."
    sh "rspec spec/functional"
  end

  desc "Run all specs"
  task :all => [:unit, :func]
end
