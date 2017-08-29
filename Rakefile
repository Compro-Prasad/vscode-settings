require 'rake'
require 'json'

desc 'Link vscode settings'
task :install do
  %w[settings.json keybindings.json snippets].each do |setting|
    link_path setting
  end

  stored_extensions = JSON.parse(File.read(extensions_file_path))
  not_yet_installed = stored_extensions - installed_extensions

  if not_yet_installed.any?
    not_yet_installed.each do |extension|
      puts "installing #{extension}"
      _result = `code --install-extension #{extension}`
    end
  else
    puts 'no new extensions to install'
  end
end

desc 'Sync installed extensions'
task :sync do
  File.open(extensions_file_path, 'w') do |f|
    f.write(JSON.pretty_generate(installed_extensions))
  end
end

def extensions_file_path
  "#{Dir.pwd}/extensions.json"
end

def installed_extensions
  `code --list-extensions`.split("\n")
end

def link_path(file)
  puts "linking #{file}"

  link, target = link_and_target(file)

  if File.exist?(link)
    skip_or_replace(link, target)
  else
    link_system_call(link, target)
  end
end

def skip_or_replace(link, target)
  if File.identical?(target, link)
    puts "identical #{link}"
  else
    print "overwrite #{link}? [ynq] "
    case $stdin.gets.chomp
    when 'y'
      replace_file(link, target)
    when 'q'
      exit
    else
      puts "skipping #{link}"
    end
  end
end

def replace_file(link, target)
  FileUtils.rm_rf(link)
  link_system_call(link, target)
end

def link_and_target(file)
  link = "#{root_path}/#{file}"
  target = "#{Dir.pwd}/#{file}"

  [link, target]
end

def link_system_call(link, target)
  if windows?
    mklink_opts = File.directory?(target) ? '/J' : ''

    link.tr!('/', '\\')
    target.tr!('/', '\\')

    system %(cmd /c mklink #{mklink_opts} "#{link}" "#{target}")
  else
    system %(ln -s "#{target}" "#{link}")
  end
end

def windows?
  RUBY_PLATFORM =~ /(win32|mingw32)/
end

def root_path
  env_root =
    if windows?
      ENV['AppData']
    else
      File.expand_path('~/Library/Application Support/')
    end

  "#{env_root}/Code/User"
end
