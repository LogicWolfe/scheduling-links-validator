desc "Builds crawler and parser binaries."
task :build do |t|
  Dir.chdir("crawler") {
    sh "go build"
  }
  Dir.chdir("parser") {
    sh "go build"
  }
  mkdir_p "bin"
  mv "crawler/crawler", "bin/"
  mv "parser/parser", "bin/"

  puts "Binaries can be found in bin/"
end

desc "Removes built binaries and build artifacts."
task :clean do |t|
  rm_r "bin/"
end

desc "Removes crawler and parser outputs."
task :clean_output do |t|
  rm Dir.glob("/tmp/crawler_output.*.sqlite")
  rm Dir.glob("/tmp/parser_output.*.sqlite")
end

desc "Creates a manifest_url file in the crawler directory, if one doesn't exist. Seeds the manifest_urls file with some test urls"
task :seed do |t|
  output = "bin/manifest_urls"
  mkdir_p "bin"
  if File.exist?(output)
    abort "#{output} already exists - please remove the file first"
  end

  # Test manifests from
  # https://docs.google.com/spreadsheets/d/1Fh0zwCjKYh4D-Mp1k5uxzINh6GG0yI1ezko49VaJV2c
  seed_manifest_urls = %w(
https://chperx-tst.health-partners.org/FHIRTST/api/epic/2021/Scheduling/Utility/covid-vaccine-availability/$bulk-publish
https://api.carbonhealth.com/hib/publicVaccination/$bulk-publish
https://www.cvs.com/immunizations/inventory/data/$bulk-publish
https://fhir.epic.com/interconnect-fhir-oauth/api/epic/2021/Scheduling/Utility/covid-vaccine-availability/$bulk-publish
https://raw.githubusercontent.com/smart-on-fhir/smart-scheduling-links/master/examples/$bulk-publish
https://raw.githubusercontent.com/jmandel/wba-appointment-fetch/gh-pages/$bulk-publish
)
  File.write(output, seed_manifest_urls.join("\n"))
  puts "#{output} seeded with #{seed_manifest_urls.length} manifest urls."
end


task :default => [:build]
