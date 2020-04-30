load("//container:container.bzl", "container_image", "container_import")
load("//docker/package_managers:download_pkgs.bzl", "download_pkgs")
load("//docker/package_managers:install_pkgs.bzl", "install_pkgs")
load("//docker/util:run.bzl", "container_run_and_commit")

download_pkgs(
    name = "download_python_debs",
    image_tar = "@ubuntu1804//image",
    packages = [
        "python3",
        "python3-pip",
        "python3-setuptools",
    ],
)

install_pkgs(
    name = "python_debs_image_base",
    image_tar = "@ubuntu1804//image",
    installables_tar = ":download_python_debs.tar",
    output_image_name = "python_debs_image_base_output",
)

container_image(
	name = "image_with_requirements_file",
	base = ":python_debs_image_base",
	files = [":requirements.txt"],
)

container_run_and_commit(
	name = "install_requirements",
	image = ":image_with_requirements_file.tar",
	commands = ["python3 -m pip install -r requirements.txt"],
)

container_image(
	name = "image",
	base = ":install_requirements",
)
