import { motion, useInView } from 'framer-motion';
import type { Easing } from 'framer-motion';
import { useRef, useState, useEffect } from 'react';
import { TypeAnimation } from 'react-type-animation';

const About = () => {
  const ref = useRef(null);
  const [startTyping, setStartTyping] = useState(false);
  const inView = useInView(ref, { once: true, margin: "-40% 0px -40% 0px" });

  useEffect(() => {
    if (inView) {
      setStartTyping(true);
    }
  }, [inView]);

  const textContainerVariants = {
    hidden: { opacity: 0 },
    visible: { opacity: 1, transition: { staggerChildren: 0.1 } },
  };

  const ease: Easing = 'easeOut';

  const textItemVariants = {
    hidden: { opacity: 0, y: 20 },
    visible: { opacity: 1, y: 0, transition: { duration: 0.5, ease } },
  };

  const mediaContainerVariants = {
    hidden: { opacity: 0 },
    visible: { opacity: 1, transition: { staggerChildren: 0.15, delayChildren: 0.2 } },
  };

  const videoVariant = {
    hidden: { opacity: 0, x: -30 },
    visible: { opacity: 1, x: 0, transition: { duration: 0.6, ease } },
  };

  const imageVariant = {
    hidden: { opacity: 0, x: 30 },
    visible: { opacity: 1, x: 0, transition: { duration: 0.6, ease } },
  };

  const scrollToSection = (id: string) => {
    const element = document.getElementById(id);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  };

  return (
    <div id="about" ref={ref} className="relative min-h-screen w-screen bg-white py-24 px-8 md:px-[10vw]">
      <motion.div
        className="grid grid-cols-1 md:grid-cols-2 gap-16 w-full h-full items-start md:items-center"
        initial="hidden"
        animate={inView ? "visible" : "hidden"}
        variants={textContainerVariants}
      >
        {/* Left Column: Text Content */}
        <motion.div 
          className="flex flex-col justify-center"
        >
          <div className="h-12 md:h-16 mb-8">
            {startTyping ? (
              <TypeAnimation
                sequence={['Hello, world...']}
                wrapper="h2"
                cursor={true}
                className="text-4xl md:text-5xl font-bold text-primary font-serif"
              />
            ) : (
              <h2 className="text-4xl md:text-5xl font-bold text-primary font-serif text-transparent">
                Hello, world...
              </h2>
            )}
          </div>
          <motion.p variants={textItemVariants} className="text-tertiary text-lg mb-6">
            I'm Joshua, a <strong>Data Science</strong> and <strong>Mathematics/Computer Science</strong> student at <strong>UC San Diego</strong> with a passion for building <strong>intelligent systems</strong> and exploring where <strong>technology meets creativity</strong>.
          </motion.p>
          <motion.p variants={textItemVariants} className="text-tertiary text-lg mb-4"><strong>I...</strong></motion.p>
          <ul className="list-disc list-inside text-tertiary text-lg mb-6 space-y-4 ml-4">
            <motion.li variants={textItemVariants}>
              am fueled by curiosity for <strong>artificial intelligence</strong> and <strong>machine learning</strong>,
            </motion.li>
            <motion.li variants={textItemVariants}>
              love solving <strong>complex problems</strong> through developing <strong>LLM algorithms</strong>, creating <strong>computer vision tools</strong>, building <strong>agentic AI systems</strong>, and more,
            </motion.li>
            <motion.li variants={textItemVariants}>
              bring experience as an <strong>AI Research Fellow</strong> and <strong>Full-Stack Developer</strong> plus extensive work with my self-hosted <strong>home lab</strong>,
            </motion.li>
            <motion.li variants={textItemVariants}>
              also find joy in tending to my <strong>aquariums</strong>, spinning my <strong>vinyl records</strong>, and unwinding at the <strong>beach</strong>.
            </motion.li>
          </ul>
          <motion.p variants={textItemVariants} className="text-tertiary text-lg">
            I'm always excited to <strong>connect with others</strong> who share my interests, whether in tech or hobbies. Feel free to{' '}
            <a onClick={() => scrollToSection('contact')} className="font-bold text-primary hover:underline cursor-pointer">
              reach out!
            </a>
          </motion.p>
        </motion.div>

        {/* Right Column: Media */}
        <motion.div 
          className="flex items-center justify-center"
          variants={mediaContainerVariants}
        >
            <div className="flex gap-4 w-full">
                <motion.div variants={videoVariant} className="w-7/12 aspect-[9/16] rounded-lg overflow-hidden bg-gray-200">
                    <video
                        src="/media/about/roomtour.mov"
                        autoPlay
                        loop
                        muted
                        playsInline
                        className="w-full h-full object-cover"
                    />
                </motion.div>
                <div className="w-5/12 flex flex-col gap-4">
                    <motion.div variants={imageVariant} className="aspect-square bg-gray-200 rounded-lg overflow-hidden">
                        <img src="/media/about/image1.png" alt="About 1" className="w-full h-full object-cover" />
                    </motion.div>
                    <motion.div variants={imageVariant} className="aspect-square bg-gray-200 rounded-lg overflow-hidden">
                        <img src="/media/about/image2.png" alt="About 2" className="w-full h-full object-cover" />
                    </motion.div>
                    <motion.div variants={imageVariant} className="aspect-square bg-gray-200 rounded-lg overflow-hidden">
                        <img src="/media/about/image3.png" alt="About 3" className="w-full h-full object-cover" />
                    </motion.div>
                </div>
            </div>
        </motion.div>
      </motion.div>
    </div>
  );
};

export default About;
