task :default => "talen:update"

namespace :talen do
  task :update do
    source_dir = File.expand_path('../../5ti5d-ruby', __FILE__)
    output_dir = File.expand_path('../5ti5d', __FILE__)
    system("rsync -av #{source_dir}/public/ #{output_dir}/")
  end
end