require 'rake'

desc 'Link vscode settings'
task :install do
  %w(settings.json keybindings.json snippets).each do |setting|
    link_path setting
  end
end

desc 'Sync extensions'
task :sync do
  # TODO: figure out a good way to sync these...
end

def link_path(file)
  puts "linking #{file}"

  link = "#{root_path}/#{file}"
  target = "#{Dir.pwd}/#{file}"

  link_system_call(link, target)
end

def link_system_call(link, target)
  if windows?
    link.tr!('/', '\\')
    target.tr!('/', '\\')

    system %(cmd /c mklink "#{link}" "#{target}")
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
